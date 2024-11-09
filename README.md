<input type="text" id="password" placeholder="Wpisz hasło do hashowania..." style="width: 300px; padding: 5px;">
<button onclick="generateHash()">Generuj Hash</button>

<pre id="hashResult" style="background: #f0f0f0; padding: 10px; border: 1px solid #ddd; margin-top: 10px;"></pre>

<script>
async function generateHash() {
    const password = document.getElementById('password').value;
    const encoder = new TextEncoder();
    const data = encoder.encode(password);
    const hashBuffer = await crypto.subtle.digest('SHA-256', data);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    const hashHex = hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
    document.getElementById('hashResult').textContent = `Hash: ${hashHex}`;
}
</script>
