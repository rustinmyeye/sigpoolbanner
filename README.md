200x25 white background

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Scrolling Ticker</title>
<style>
    body {
        margin: 0;
        padding: 0;
    }

    #ticker {
        width: 200px;
        height: 25px;
        overflow: hidden;
        position: relative;
        background-color: white;
        color: #FF5537;
        font-family: 'Roboto', sans-serif; /* Using Roboto font from Google Fonts */
        white-space: nowrap; /* ensures text stays on one line */
        font-weight: bold;
        text-shadow: 1px 1px 1px #58585A;
    }

    #ticker::before {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: calc(20px - 10px); /* Adjust as needed */
        height: 100%;
        background-color: #58585A; /* Medium gray color matching the logo */
        z-index: 1; /* Ensure it's behind the logo */
        clip-path: polygon(100% 0, 80% 100%, 0% 100%, 0 0); /* Clip the left side of the pseudo-element */
    }

    #ticker p {
        display: inline-block;
        animation: ticker 14s linear infinite; /* duration slightly faster */
        margin: 0; /* removes default margin */
        padding-left: 0px; /* Add padding to ensure text is not overlapped by the logo */
        line-height: 25px; /* Center the text vertically within the ticker height */
    }

    @keyframes ticker {
        0% { transform: translateX(100%); }
        100% { transform: translateX(-100%); }
    }

    #ticker img {
        position: absolute;
        left: -2px; /* positioned to the left */
        top: 0;
        height: 100%; /* Use full height of the ticker */
        z-index: 2; /* ensures it's on top */
        clip-path: polygon(0 0, 100% 0, 80% 100%, 0% 100%); /* Clip the image on an angle */
    }
</style>
</head>
<body>

<div id="ticker">
    <img src="https://sigmanauts.com/img/sigmanaut-logo.png" alt="logo">
    <p>Quick, FREE payouts | DAO driven open mining pool | Hourly Bonus Token Payments</p>
</div>

</body>
</html>

Pool hashrate and miner count


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scrolling Ticker</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #fff; /* Default background color */
            color: #000; /* Default text color */
        }

        @media (prefers-color-scheme: dark) {
            body {
                background-color: #000; /* Dark mode background color */
                color: #fff; /* Dark mode text color */
            }
        }

        #ticker {
            width: 100%;
            height: 50px;
            overflow: hidden;
            position: relative;
            background-color: transparent; /* Transparent background */
            font-family: 'Roboto', sans-serif; /* Using Roboto font from Google Fonts */
            white-space: nowrap; /* ensures text stays on one line */
            display: flex;
            align-items: center; /* vertically center items */
        }

        #ticker::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            width: calc(50% - 10px); /* Adjust as needed */
            height: 100%;
            background-color: #58585A; /* Medium gray color matching the logo */
            z-index: 1; /* Ensure it's behind the logo */
            clip-path: polygon(100% 0, 80% 100%, 0% 100%, 0 0); /* Clip the left side of the pseudo-element */
        }

        #ticker p {
            display: inline-block;
            animation: ticker 10s linear infinite; /* duration slightly faster */
            margin: 0; /* removes default margin */
            padding-left: 20px; /* Add padding to ensure text is not overlapped by the logo */
            position: relative; /* Relative positioning for absolute positioning of text */
        }

        #ticker .sigmanauts-text {
            color: #000; /* Black text color for "Sigmanauts" */
            position: absolute; /* Position "Sigmanauts" absolutely within the ticker */
            top: 50%; /* Align "Sigmanauts" to the middle vertically */
            transform: translateY(-50%); /* Adjust vertical alignment */
            left: calc(100% + 10px); /* Position "Sigmanauts" to the right of the ticker */
            white-space: nowrap; /* Ensure "Sigmanauts" stays on one line */
        }

        @keyframes ticker {
            0% { transform: translateX(100%); }
            100% { transform: translateX(-100%); }
        }

        #ticker img {
            position: absolute;
            left: 10px; /* positioned to the left */
            top: 0;
            height: 100%; /* Use full height of the ticker */
            z-index: 2; /* ensures it's on top */
            clip-path: polygon(0 0, 100% 0, 80% 100%, 0% 100%); /* Clip the image on an angle */
        }
    </style>
</head>
<body>

<div id="ticker">
    <img src="https://sigmanauts.com/img/sigmanaut-logo.png" alt="logo">
    <p id="tickerText"></p> <!-- Changed id to "tickerText" -->
</div>

<script>
    // Fetch data from the API endpoint for pool hashrate
    fetch('https://api.codetabs.com/v1/proxy/?quest=http://15.204.211.130:4000/api/pools/ErgoSigmanauts/performance')
        .then(response => response.json())
        .then(data => {
            // Extract the most recent pool hashrate
            const latestStats = data.stats[data.stats.length - 1];
            const poolHashrate = latestStats.poolHashrate / 1000000000; // Convert to GH/s

            // Update the HTML element with the pool hashrate
            document.getElementById('tickerText').textContent = `Pool Hashrate: ${poolHashrate.toFixed(2)} GH/s`;
        })
        .catch(error => {
            console.error('Error fetching pool hashrate:', error);
        });

    // Fetch data from the API endpoint for connected miners
    fetch('https://api.codetabs.com/v1/proxy/?quest=http://15.204.211.130:4000/api/pools/ErgoSigmanauts/miners?pageSize=5000')
        .then(response => response.json())
        .then(data => {
            // Get the number of connected miners
            const connectedMiners = data.length;

            // Update the HTML element with the number of connected miners
            document.getElementById('tickerText').textContent += ` | Connected Miners: ${connectedMiners}`;
        })
        .catch(error => {
            console.error('Error fetching connected miners:', error);
        });
</script>

</body>
</html>

