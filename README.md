# Discord hypesquad badges
Allows you to get discord hypesquad badges after they were removed from client.

# Steps:

1. Navigate to discord in your browser and login
   Press F12, a developer tools will open on right or bottom
   Navigate to "Console" tab
   Type "allow pasting" (without quotes) if your browser requires it
```
   // Change this based on the hypesquad you want "bravery", "brilliance", or "balance"
   const house = "brilliance";

   (async () => {
    // this part gets your discord token, it does not send it anywhere
    // credits for this code snippet to https://gist.github.com/XielQs/90ab13b0c61c6888dae329199ea6aff3
    let token;
    window.webpackChunkdiscord_app.push([[Symbol()], {}, o => {
        for (let e of Object.values(o.c)) {
            try {
                if (!e.exports || e.exports === window) continue;
                if (e.exports?.getToken) {
                    token = e.exports.getToken();
                }
                for (let o in e.exports) {
                    if (e.exports?.[o]?.getToken && "IntlMessagesProxy" !== e.exports[o][Symbol.toStringTag]) {
                        token = e.exports[o].getToken();
                    }
                }
            } catch {}
        }
    }]);
    window.webpackChunkdiscord_app.pop();

    if (!token) {
        console.error("Failed to retrieve token");
        return;
    }

    console.log("Token successfully retrieved");
   
    const houses = ["bravery", "brilliance", "balance"];
    if (!houses.includes(house.toLowerCase())) {
        console.error("Invalid house! Please, use: bravery / brilliance / balance");
        return;
    }

    const houseId = houses.indexOf(house.toLowerCase()) + 1;

    // this part of code sends request to discord api, setting your hypesquad
    // (Authorization header is set to your token so it sets it on your account)
    // Your token is never send outside of discord.
    try {
        const response = await fetch("https://discord.com/api/v9/hypesquad/online", {
            method: "POST",
            headers: {
                "Authorization": token,
                "Content-Type": "application/json"
            },
            body: JSON.stringify({ house_id: houseId })
        });

        if (response.status === 204) console.log(`Successfully activated your HYPESQUAD house to: ${house}`);
        else console.error("Failed to change house");
    } catch (err) {
        console.error(err);
    }
})();
```
