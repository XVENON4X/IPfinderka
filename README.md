# IP Finder by VENOM

Wprowadź poniżej nick do wyszukania w pliku `0001.txt`.

<input type="text" id="searchTerm" placeholder="Wpisz nick..." style="width: 300px; padding: 5px; margin-top: 10px;">
<button onclick="searchInFile()" style="padding: 5px 10px; cursor: pointer; margin-left: 10px;">Wyszukaj w pliku</button>

<pre id="results" style="background: #f5f5f5; padding: 15px; border-radius: 5px; margin-top: 20px; max-height: 300px; overflow-y: auto;"></pre>

<script>
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

        // Optymalizacja wyszukiwania: Przerwij po znalezieniu pierwszego dopasowania
        for (let index = 0; index < lines.length; index++) {
            const line = lines[index];
            if (line.toLowerCase().includes(searchTerm.toLowerCase())) {
                resultsArea.textContent = `Linia ${index + 1}: ${line}`;
                found = true;
                break; // Przerwij pętlę po znalezieniu
            }
        }

        if (!found) {
            resultsArea.textContent = "Nie znaleziono takiego nicku.";
        }
    } catch (error) {
        resultsArea.textContent = "Wystąpił błąd: " + error.message;
    }
}
</script>
