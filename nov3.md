select * from db.schemna.table a
left join(db.schema.table) b  b.coulmname = left(a.coluname, 4)


AIM
[secExpense].[sec].[ObserverMapping] table need to updated the PanchWardCode to the ward code for candidate's need to be added for that  observr Auto_id. How we get this code is below
Backinfo

there are following tables in sec and secExpense database
such as
⦁   sec.sec.CandidatePersonalInfo #for panchwardcode
SELECT TOP (10)
AUTO_ID,
VOTER_NAME,
VOTER_NAME_ENG,
PANCHAYAT_CODE,
MOBILE_NUMBER,
AgentMobile,
AgentName
from sec.sec.CandidatePersonalInfo
⦁   secExpense.secObserverInfo #for Observer no list
⦁   secExpense.sec.ObserverMapping #for
Auto_ID ObserverName    ObserverDesignation ObserverContact Active  Pritype
1   Sh. Mast Ram    Joint Controller    9418011750  Y   003
2   Sh. Hamender Kumar  Deputy Controller   9418485131  Y   003
3   Sh. Diwakar Sharma  Deputy Controller   9882380628  Y   003
4   Sh. Ajay Kumar Verma    Deputy Controller   9418668045  Y   003
5   Sh. Harish Thakur   Deputy Controller   8219280264  Y   003
6   Sh. Sanjeev Mahajan Law Officer, SECHP  9418025440  Y   001

Steps
Test

📱 ObserverDashboardPage.xaml.cs
    ↓ picker_wards_SelectedIndexChanged()
    ↓ Gets selected ward's Panchayat_Code
    
🌐 API Call: ObserverCandidates_Get()
    ↓ URL: baseurl + "api/ObserverCandidates?PanchWardCode={encrypted_code}"
    ↓ Controller: ObserverCandidatesController.cs
    
🗄️  Stored Procedure: sec.Mobile_getobserver_candidates
    ↓ Parameters: @PanchWardCode (e.g., '1309001001')
    ↓ Query: SELECT i.AUTO_ID, i.VOTER_NAME, SUM(c.amount) Amount
    ↓        FROM sec.CandidatePersonalInfo i
    ↓        LEFT JOIN sec.candidateRegister c ON c.AutoID = i.AUTO_ID
    ↓        WHERE CONSTITUENCY_CODE = @PanchWardCode
    ↓        AND c.ExpStatus = 'F'
    
📱 Local Storage: ObserverCandidatesDatabase.AddObserverCandidates()
    ↓ Displays candidates in listView_candidatedetails


