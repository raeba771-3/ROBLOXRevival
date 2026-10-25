# Studio Hosting



So i'll be making a guide for people who wanna make a revival or just play an older version of roblox yeah lol let's get started

it's gonna be short

Technically, what is Studio Hosting ? Studio Hosting  replaces RCCService ( because in 2021 versions and later there's no RCCService available so people block at it) and with Studio Hosting you can play or make revivals of *2021 versions and later, (until April 2023 because unfortunately Roblox implemented its Hyperion system) and yeah that's it


To put it simply, it's a server. okay ?


First, you need a RobloxStudioBeta.exe which is already patched. ( there is a guide : https://github.com/idontknowwhattoputxd/Roblox-2022-Guides/tree/main/Login)

then, you're gonna make a folder on your desk, put whatever name to it idc
put your patched studio (exe) in it


now, in your folder, you right-click, then new → text document
make sure to rename it to "launch-server.bat"...actually you can put whatever name to it, it isn't really important
but there is one thing that is important ⚠️ MAKE SURE THAT IT'S .bat AND NOT .bat.txt ⚠️
right-click the file and edit, you can put my code:
(@echo off
title Roblox 2022 Studio Hosting Server
echo Launching Patched Roblox Studio 2022 in Server Mode...
:: Force Studio into a headless-like server instance listening on port 53640
RobloxStudioBeta.exe -Server -Port 53640 -BaseplaceId 0 -volauncher
pause) ( dont put the parentheses when writing the code)

save it


😀

Normally, if this is a Revival for just you, you can stop here, but if you want to play with your friends, read this guide to the end. at the end, reguardless if you use it alone or with people, i'll show you how to make a server.



HOW TO CREATE THE FREE NETWORK TUNNEL(optional): (this guide is made by myself 😎😎)

so first, go to Playit.gg, and download the free client from it ig
then, run the program, it will open a browser link for setting up your account.
click add tunnel, to the dashboard
select UDP as the protocol (Roblox traffic relies on UDP)
set the localport to 53640
Playit will generate u a permanent adress so make sure to copy this !!!
umm that's it i guess


CODING THE BACKEND !!! ( API and JoinScript) (OBLIGATORY) :

create a file named ''server.js'' or whatever, it just need to be in your project file
then, copy & paste this code : 
const express = require('express');
const app = express();
const PORT = 8000;

// The tunnel details you generated using Playit.gg in Step 3
const TUNNEL_IP = "your-revival.playit.gg";
const TUNNEL_PORT = 12345;

// Route called by the Roblox Client when a player clicks "Play"
app.get('/Game/PlaceLauncher.ashx', (req, res) => {
    res.setHeader('Content-Type', 'text/plain');
    
    // The structural JoinScript sent directly to the client
    const joinScript = `
        local NetworkClient = game:GetService("NetworkClient")
        local Players = game:GetService("Players")
        
        -- Create a clean local player entity
        local player = Players:CreateLocalPlayer(0)
        player.Name = "RevivalGuest"
        
        -- Fire connection sequence to the hosted Studio instance
        NetworkClient:Connect("${TUNNEL_IP}", ${TUNNEL_PORT}, 0, 20)
    `;
    
    res.send(joinScript);
});

app.listen(PORT, () => {
    console.log(`[API] Revival Backend routing live on http://localhost:${PORT}`);
});


********

if you play it alone delete the paragraph with ''//the tunnel details....''


FINALLY, THE BOOT SEQUENCE ORDER !!!!:

so to avoid client connection drops, always launch these components in this exact order :
1/Start your Backend API: Run node server.js so localhost:8000 is ready to intercept incoming requests.
2/Start Playit.gg: Open the tunnel client to begin forwarding network packets
3/Launch the Server: Double-click start_server.bat. A minimal, static Studio screen or terminal log will appear



IT'S THE ENDDDD :))))))



