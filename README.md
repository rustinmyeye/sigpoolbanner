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
    }

    #ticker {
        width: 100%;
        height: 50px;
        overflow: hidden;
        position: relative;
        background-color: white;
        color: black;
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
        width: calc(30% - 10px); /* Adjust as needed */
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
    }

    @keyframes ticker {
        0% { transform: translateX(100%); }
        100% { transform: translateX(-100%); }
    }

    #ticker img {
        position: absolute;
        left: 18px; /* positioned to the left */
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
