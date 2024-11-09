<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XOR Encryption in JavaScript</title>
</head>
<body>
    <h1>Szyfrowanie XOR w JavaScript</h1>
    <p id="encrypted">Zaszyfrowane dane: <span id="encrypted-text"></span></p>
    <p id="decrypted">Deszyfrowane dane: <span id="decrypted-text"></span></p>

    <script>
        // Funkcja szyfrowania / deszyfrowania XOR
        function xorEncryptDecrypt(data, key) {
            let result = '';
            for (let i = 0; i < data.length; i++) {
                result += String.fromCharCode(data.charCodeAt(i) ^ key);
            }
            return result;
        }

        // Zaszyfrowane dane w postaci tekstu
        const encryptedData = '¼ÓÛÞÖçÕ';  // Zaszyfrowane dane z Pythona: 'Testowy tekst do zaszyfrowania' z kluczem XOR=123

        // Klucz XOR
        const key = 123;

        // Deszyfrowanie danych
        const decryptedData = xorEncryptDecrypt(encryptedData, key);

        // Wyświetlanie zaszyfrowanych i deszyfrowanych danych w HTML
        document.getElementById('encrypted-text').textContent = encryptedData;
        document.getElementById('decrypted-text').textContent = decryptedData;
    </script>
</body>
</html>
