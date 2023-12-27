# Tugas-13-PBKK

## Adhira Riyanti Amanda - 5025211102

### Google App Script
```js
const DATA_ENTRY_SHEET_NAME = "Sheet1";
var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(DATA_ENTRY_SHEET_NAME);

const doPost = (request = {}) => {
  const {postData: {contents, type} = {} } = request;
  var data = parseFormData(contents);
  appendToGoogleSheet(data);
  return ContentService.createTextOutput(contents).setMimeType(ContentService.MimeType.JSON);
}

function parseFormData(postData){
  var data={};
  var parameters = postData.split('&');
  for (var i=0; i<parameters.length; i++){
    var keyValue = parameters[i].split('=');
    var key = decodeURIComponent(keyValue[0].replace(/\+/g, ' '));
    var value = decodeURIComponent(keyValue[1].replace(/\+/g, ' '));
    data[key] = value;
  }
  return data;
}

function appendToGoogleSheet(data){
  var headers = sheet.getRange(1,1,1, sheet.getLastColumn()).getValues()[0];
  var rowData = headers.map(headerFld => data [headerFld]);
  sheet.appendRow(rowData);
}
```