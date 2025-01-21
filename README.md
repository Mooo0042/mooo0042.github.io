<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Abstimmung</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 50px; }
        button { margin: 5px; padding: 10px 20px; font-size: 16px; }
    </style>
</head>
<body>
    <h1>Abstimmung</h1>
    <p>Wähle deine Option:</p>
    <button onclick="vote('Option 1')">Option 1</button>
    <button onclick="vote('Option 2')">Option 2</button>
    <button onclick="vote('Option 3')">Option 3</button>

<h2>Ergebnisse</h2>
    <pre id="results">Lade Ergebnisse...</pre>

<script>
        async function fetchResults() {
            const response = await fetch('results.json');
            const data = await response.json();
            document.getElementById('results').innerText = JSON.stringify(data, null, 2);
        }

        async function vote(option) {
            await fetch('https://api.github.com/repos/Mooo0042/mooo0042.github.io/dispatches', {
                method: 'POST',
                headers: {
                    'Authorization': 'Bearer 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',
                    'Accept': 'application/vnd.github.everest-preview+json',
                },
                body: JSON.stringify({ event_type: 'vote', client_payload: { option } })
            });
            alert('Stimme abgegeben!');
        }

        fetchResults();
    </script>
</body>
</html>
