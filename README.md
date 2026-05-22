# Cadastro de Artistas

O `index.html` carrega a lista do Google Sheets pelo Web App do Google Apps Script configurado em `GOOGLE_SCRIPT_URL`.

Para a listagem funcionar, o Apps Script precisa responder ao `GET` com JSON. Exemplo:

```js
function doGet() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const values = sheet.getDataRange().getValues();
  const headers = values.shift();
  const artistas = values.map(row => {
    return headers.reduce((obj, header, index) => {
      obj[header] = row[index];
      return obj;
    }, {});
  });

  return ContentService
    .createTextOutput(JSON.stringify({ artistas }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

O botão `Baixar JSON` continua exportando os dados que estão sendo exibidos na tela.
