# IP Finder by VENOM

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
// Wprowadź tutaj poprawny hash, który wygenerowałeś dla hasła "pozdro213"
const encryptedPassword = "TWOJ_WYGENEROWANY_HASH_TUTAJ"; // Upewnij się, że jest to poprawny hash

async function hashPassword(password) {
    const encoder = new TextEncoder();
    const data = encoder.encode(password);
    const hashBuffer = await crypto.subtle.digest('SHA-256', data);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

async function login() {
    const password = document.getElementById('password').value.trim();
    const hashedInput = await hashPassword(password);

    if (hashedInput === encryptedPassword) {
        alert("Zalogowano pomyślnie!");
        document.getElementById('searchSection').style.display = 'block';
    } else {
        alert("Błędne hasło!");
    }
}
</script>
