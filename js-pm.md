// Generate Basic Auth Token

const rawAuth = "3O%2BMVC0RSgx0klSvZ4%2Fpcw%3D%3D:2uS7yDJy02QGCywWXsEx7aVd%2BjrDBhbERipESVk%2BRcU%3D";

const basicAuthToken = CryptoJS.enc.Base64.stringify(CryptoJS.enc.Utf8.parse(rawAuth));

pm.collectionVariables.set("basicAuthToken", basicAuthToken);



console.log("Basic Auth Token generated:", basicAuthToken);



// Encryption Key

const encryptionKey = "5gS2E70CA13935B9";



// Get variables from collection (you can set these in collection variables)

const aadhaarNumber = pm.collectionVariables.get("aadhaarNumber") || "123456789012";

const aadhaarName = pm.collectionVariables.get("aadhaarName") || "Test Name";



// Create the payload to be encrypted

const payload = {

    password: "Welcome@123",

    aadhaarNumber: aadhaarNumber,

    txnRequestID: pm.variables.replaceIn('{{$guid}}'),

    bioAuth: "n",

    demoAuth: "y",

    name: aadhaarName

};



console.log("Payload before encryption:", JSON.stringify(payload));



// AES Encryption function (matching C# implementation)

function encryptData(data, key) {

    // Convert key to proper format (assuming it's a hex string or UTF-8)

    const keyUtf8 = CryptoJS.enc.Utf8.parse(key);

    

    // Encrypt using AES

    const encrypted = CryptoJS.AES.encrypt(data, keyUtf8, {

        mode: CryptoJS.mode.ECB,

        padding: CryptoJS.pad.Pkcs7

    });

    

    return encrypted.toString();

}



// Encrypt the payload

const jsonData = JSON.stringify(payload);

const encryptedData = encryptData(jsonData, encryptionKey);



// Set encrypted data as collection variable

pm.collectionVariables.set("encryptedData", encryptedData);



console.log("Encrypted data set successfully");