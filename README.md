<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>IP Finder by VENOM</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #007bff;
        }
        input, button, textarea {
            margin: 10px 0;
        }
        textarea {
            width: 80%;
            height: 200px;
            resize: none;
        }
        button {
            cursor: pointer;
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>IP Finder by VENOM</h1>
    <label for="searchTerm">Nick do wyszukania:</label>
    <input type="text" id="searchTerm" placeholder="Wpisz nick..." />
    <button onclick="searchInFile()">Wyszukaj w pliku</button>
    <textarea id="results" readonly placeholder="Wyniki wyszukiwania..."></textarea>
    <script>
        // Funkcja do wyszukiwania w pliku 0001.txt
        async function searchInFile() {
            const searchTerm = document.getElementById('searchTerm').value.trim();
            const resultsArea = document.getElementById('results');
            resultsArea.value = ""; // Czyszczenie wyników
            if (!searchTerm) {
                alert("Podaj słowo do wyszukania.");
                return;
            }
            try {
                // Wczytywanie zawartości pliku 0001.txt
                const response = await fetch('0001.txt');
                if (!response.ok) {
                    alert("Nie można otworzyć pliku 0001.txt");
                    return;
                }
                const fileContent = await response.text();
                const lines = fileContent.split('\n');
                let found = false;
                // Przeszukiwanie pliku
                lines.forEach((line, index) => {
                    if (line.toLowerCase().includes(searchTerm.toLowerCase())) {
                        resultsArea.value += `Linia ${index + 1}: ${line}\n`;
                        found = true;
                    }
                });
                if (!found) {
                    resultsArea.value = "Nie znaleziono takiego nicku.";
                }
            } catch (error) {
                alert("Wystąpił błąd: " + error.message);
            }
        }
    </script>
</body>
</html>
