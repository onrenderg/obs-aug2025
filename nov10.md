

```sql
USE [DigitalNagrik]
GO

-- Declare output parameters
DECLARE @status_code INT
DECLARE @status_message NVARCHAR(200)
DECLARE @UserID INT
DECLARE @UserProfileID INT

-- Execute the stored procedure with test values
EXEC [dbo].[API_OTP_Put]
    @UserMobile = '9876543210',      -- Replace with actual mobile number
    @OTP_ID = 123,                   -- Replace with actual OTP ID from OTPLog table
    @OTP = 1234,                     -- Replace with actual OTP value
    @status_code = @status_code OUTPUT,
    @status_message = @status_message OUTPUT,
    @UserID = @UserID OUTPUT,
    @UserProfileID = @UserProfileID OUTPUT

-- Display the results
SELECT 
    @status_code AS StatusCode,
    @status_message AS StatusMessage,
    @UserID AS UserID,
    @UserProfileID AS UserProfileID
GO
```



```sql
-- Find recent unverified OTPs
SELECT TOP 5 
    OTPId, 
    MobileNo, 
    OTP, 
    CreatedDateTime,
    VerifiedDateTime
FROM OTPLog 
WHERE VerifiedDateTime IS NULL
ORDER BY CreatedDateTime DESC
```


```sql
USE [DigitalNagrik]
GO
/****** Object:  StoredProcedure [dbo].[API_OTP_Post]    Script Date: 10-11-2025 11:57:58 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
ALTER procedure [dbo].[API_OTP_Post]
(
@UserMobile	char(10),
--API Input Parameters (Not Requred For Web)
@status_code int  = 201 OUTPUT,
@status_message NVARCHAR(200)  = 'OK' OUTPUT,
@otp_id int = 1 out,
@otp_value int = 1 out,
@otp_message varchar(300) = '' out,
@otp_entityid varchar(50) = '1401481550000045818' out,
@otp_tmpid varchar(50) = '1407167386460654881' out,
@otp_username varchar(50)= 'gacgov.otp' out,
@otp_password varchar(50)= 'D4%gM6$tD8' out,
@otp_senderid varchar(50)= 'GACGOV' out
)

as
begin
    declare @otp int = CAST((RAND() * (899999) + 100000) as int);
	--TEMPORARY Code For OTP 123456
	    set @otp = 123456; 
	--END TEMPORARY Code For OTP 123456
    begin
        insert into OTPLog(MobileNo,OTP,OTPDateTime)
        values(@UserMobile,@otp,GETDATE())
    end
    --Parameters for API 
    set @otp_id = SCOPE_IDENTITY()
    set @otp_value = @otp;
	 set @otp_message ='Dear User, OTP for logging into https://gac.gov.in is '+ cast(@OTP as varchar)  +'. Do not share with anyone.';
	
    --set @otp_message = 'OTP for mobile verification is ' + cast(@otp_value as varchar)  +' with OTP ID is ' + cast(@otp_id as varchar);
    
    set @status_code = 201;
    set @status_message = 'OTP Generated Sucessfully';
    
    set @otp_entityid = '1001649760139311252';
    set @otp_tmpid = '1007534756841924849';
    set @otp_username = 'aghpcm.sms';
    set @otp_password = '87e59xda';
    set @otp_senderid = 'HIMCMO';
    --END Parameters for API 
end

```



```sql
USE [DigitalNagrik]
GO
/****** Object:  StoredProcedure [dbo].[API_OTP_Put]    Script Date: 10-11-2025 12:11:13 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
ALTER procedure [dbo].[API_OTP_Put]
(
@UserMobile	varchar(10),
@OTP_ID	int,
@OTP	int,
@status_code int  = 200 OUTPUT,
@status_message NVARCHAR(200)  = 'OK' OUTPUT,
@UserID int  = 0 OUTPUT,
@UserProfileID int = 0 OUTPUT
)
as
begin	
	if exists(select 'X' from OTPLog where OTPId =@OTP_ID and MobileNo =@UserMobile and OTP =@OTP and VerifiedDateTime is null)
		begin
			update OTPLog set VerifiedDateTime = GETDATE() where OTPId =@OTP_ID and MobileNo  =@UserMobile and OTP =@OTP and VerifiedDateTime is null
            --Create/Check User Exists
            if not exists(select 'X' from CitizenProfile where UserMobile =@UserMobile )
            begin
                SET @UserID = (select isnull(max(UserId),0)+1 from CitizenProfile);
                SET @UserProfileID  = (select ISNULL(max(UserProfilleId),0)+1 from CitizenProfile where UserMobile =@UserMobile);

                INSERT INTO CitizenProfile (UserMobile,UserId,UserProfilleId ,IsActive,CreatedOn)
                values(@UserMobile,@UserId,@UserProfileId ,'Y',getdate())
            end
            else
            begin
                SET @UserID = (SELECT UserId from CitizenProfile where UserMobile =@UserMobile);
                SET @UserProfileID = (SELECT UserProfilleId from CitizenProfile where UserMobile =@UserMobile);
            end

            set @status_code = 200;
            set @status_message = 'OTP Verified Sucessfully';
            
        end	
    ELSE
        BEGIN
            set @status_code = 400;
            set @status_message = 'Invaid OTP Entered';
            SET @UserID = 0;
            SET @UserProfileID = 0;
        END
    END

```



## Table 

```sql
USE [DigitalNagrik]
GO

/****** Object:  Table [dbo].[OTPLog]    Script Date: 10-11-2025 12:30:34 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[OTPLog](
	[OTPId] [int] IDENTITY(1,1) NOT NULL,
	[MobileNo] [char](10) NULL,
	[Email] [varchar](100) NULL,
	[OTP] [int] NOT NULL,
	[OTPDateTime] [datetime] NOT NULL,
	[VerifiedDateTime] [datetime] NULL,
 CONSTRAINT [PK_OTPLog] PRIMARY KEY CLUSTERED 
(
	[OTPId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO



```

```sql
USE [DigitalNagrik]
GO

/****** Object:  Table [dbo].[CitizenProfile]    Script Date: 10-11-2025 12:40:31 ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[CitizenProfile](
	[UserId] [int] NOT NULL,
	[UserProfilleId] [int] NOT NULL,
	[UserName] [varchar](100) NULL,
	[FirstName] [varchar](100) NULL,
	[MiddleName] [varchar](100) NULL,
	[LastName] [varchar](100) NULL,
	[UserMobile] [varchar](10) NULL,
	[UserEmail] [varchar](100) NULL,
	[Address] [varchar](200) NULL,
	[LandMark] [varchar](100) NULL,
	[Tehsil] [varchar](50) NULL,
	[DistrictId] [int] NULL,
	[StateId] [int] NULL,
	[PinCode] [char](6) NULL,
	[Password] [varchar](64) NULL,
	[MobileVerified] [char](1) NULL,
	[EmailVerified] [char](1) NULL,
	[IsActive] [char](1) NOT NULL,
	[CreatedOn] [datetime] NOT NULL,
	[UpdatedOn] [datetime] NULL,
	[Occupation] [varchar](100) NULL,
	[LoginByMorE] [char](1) NULL,
	[AadhaarVerificationStatus] [char](1) NULL,
	[CreatedByIP] [varchar](50) NULL,
	[ModifiedByIP] [varchar](50) NULL,
	[GenderCd] [char](1) NULL,
 CONSTRAINT [PK_CitizenProfile] PRIMARY KEY CLUSTERED 
(
	[UserId] ASC,
	[UserProfilleId] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO



```