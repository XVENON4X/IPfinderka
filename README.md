# IP Finder by VENOM1.5

## Logowanie
<input type="password" id="password" placeholder="Wpisz hasło..." style="width: 300px; padding: 5px; margin-top: 10px;">
<button onclick="login()" style="padding: 5px 10px; cursor: pointer; margin-left: 10px;">Zaloguj się</button>

<div id="searchSection" style="display: none;">
    <h3>Wyszukaj nick:</h3>
    <input type="text" id="searchTerm" placeholder="Wpisz nick..." style="width: 300px; padding: 5px; margin-top: 10px;">
    <button onclick="searchInFile()" style="padding: 5px 10px; cursor: pointer; margin-left: 10px;">Wyszukaj w pliku</button>

    <pre id="results" style="background: #f5f5f5; padding: 15px; border-radius: 5px; margin-top: 20px; max-height: 300px; overflow-y: auto;"></pre>
</div>

<script>
// Zaszyfrowane hasło dla "pozdro213" (SHA-256)
const encryptedPassword = "d249ef35f662a345fbe1bdf8d730c81ff18382c8d45014478770d199b29780d3";

// Funkcja haszująca dla porównania hasła
async function hashPassword(password) {
    const encoder = new TextEncoder();
    const data = encoder.encode(password);
    const hashBuffer = await crypto.subtle.digest('SHA-256', data);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Funkcja logowania
async function login() {
    const password = document.getElementById('password').value;
    const hashedInput = await hashPassword(password);

    if (hashedInput === encryptedPassword) {
        alert("Zalogowano pomyślnie!");
        document.getElementById('searchSection').style.display = 'block';
    } else {
        alert("Błędne hasło!");
    }
}

// Funkcja do wyszukiwania w pliku 0001.txt z GitHuba
async function searchInFile() {
    const searchTerm = document.getElementById('searchTerm').value.trim();
    const resultsArea = document.getElementById('results');
    resultsArea.textContent = ""; // Czyszczenie wyników

    if (!searchTerm) {
        alert("Podaj słowo do wyszukania.");
        return;
    }

    try {
        // Wczytywanie zawartości pliku z cache
        const response = await fetch('https://raw.githubusercontent.com/XVENON4X/IPfinderka/refs/heads/main/0001.txt', { cache: 'force-cache' });
        
        if (!response.ok) {
            resultsArea.textContent = "Nie można otworzyć pliku 0001.txt";
            return;
        }
        
        const fileContent = await response.text();
        const lines = fileContent.split('\n');
        let found = false;

        // Przeszukiwanie całego pliku i wyświetlanie wszystkich dopasowań
        lines.forEach((line, index) => {
            if (line.toLowerCase().includes(searchTerm.toLowerCase())) {
                resultsArea.textContent += `Linia ${index + 1}: ${line}\n`;
                found = true;
            }
        });

        if (!found) {
            resultsArea.textContent = "Nie znaleziono takiego nicku.";
        }
    } catch (error) {
        resultsArea.textContent = "Wystąpił błąd: " + error.message;
    }
}
</script>
