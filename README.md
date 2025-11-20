# **Jetson Nano Remote Desktop**

This is a repository containing a jetson nano remote desktop using different network

---

## **Description**

Install Tailscale on the Jetson Nano and on your laptop. Once both devices are connected to Tailscale, they appear in the same private network. Use the Jetson Nano’s Tailscale IP (100.x.x.x) in NoMachine. NoMachine connects through Tailscale, giving you secure remote desktop access from anywhere in the world.

---

## **Table Of Content**

- [Installation](#installation)
- [Screenshot](#screenshot)
- [Simulator](#simulator)

---

## **Installation**

## **PART 1 – Install & connect Tailscale (private VPN)**

## **(a) Create a Tailscale account**

    1.Go to tailscale.com in your browser.

    2.Click Get Started / Sign up.

    3.Sign up with Google / Microsoft / GitHub (anything is fine).

    4.After signup, you’ll see the Tailscale admin console (list of devices).

## **(b) Install Tailscale on the server (Linux / Jetson Nano)**

**(1)** On Ubuntu / Debian / Jetson Nano:

**(2)** Open Terminal on the server.

    Run (for Debian/Ubuntu-based):

    curl -fsSL https://tailscale.com/install.sh | sh


**(3)** After install, bring it up:

    sudo tailscale up


**(4)** The terminal will show a URL, something like:

    To authenticate, visit: https://login.tailscale.com/a/XXXXXXXX


**(5)** Open that URL in your browser (on any device where you’re logged in to Tailscale), then approve the device.

**(6)** Back in the terminal, check status:

    tailscale status


You should see your server listed with an IP like 100.x.x.x (this is the Tailscale IP).

🔑 Important: Note your server’s Tailscale IP, e.g. 100.64.23.10. We’ll use this in NoMachine.

## **b. Install Tailscale on the client (Windows)**

**(1)** On your Windows PC, open browser → go to tailscale.com/download.

**(2)** Download Tailscale for Windows and install it.

**(3)** After install, Tailscale icon appears in the system tray (near the clock).

**(4)** Click the Tailscale icon → Log in… and use the same account as your server.

**(5)** After logging in, you should see “Connected”.

**(6)** To see devices:

    Right-click Tailscale icon → Admin Console → Tailscale opens in browser and shows all your devices (Windows + Jetson/server).

    Now both machines are on the same private Tailscale network.

## **c. Test Tailscale connection**

**== On Windows client : ==**

**(1)** Press Win + R, type cmd, press Enter.

**(2)** Try pinging the server’s Tailscale IP:

    ping 100.xx.xx.xx


**(2.2)** If it replies, Tailscale is good.

**(2.3)** If not:

    Make sure Tailscale is connected on both devices.

    On Linux, you can also try:

    sudo tailscale status

## **PART 2 – Install NoMachine on both sides**

**== NoMachine does the remote desktop; Tailscale is just the secure network. ==**

## **a. Install NoMachine on the server (Linux / Jetson)**

**(1)** Go to nomachine.com/download from the server’s browser.

**(2)** Download the NoMachine for Linux package (.deb for Ubuntu/Jetson based on Debian).

**(3)** Install it, e.g.:

    sudo dpkg -i nomachine_*.deb
    sudo apt-get install -f   # if there are missing dependencies


**(4)** After install, the NoMachine server service usually starts automatically.

    Check it:
    sudo /usr/NX/bin/nxserver --status


You should see something like “NoMachine – nxserver is running”.

By default, NoMachine listens on port 4000 (NX protocol).

## **b. Install NoMachine on the client (Windows)**

**(1)** On Windows, go to nomachine.com/download.

**(2)** Download NoMachine for Windows and install it with default options.

**(3)** After install, run NoMachine from the Start menu.

## **PART 3 – Configure NoMachine for Tailscale**

## **a. Get server username**

**(1)** On the server (Linux), you need to know the username you’ll log in with.

**(1.1)** Run:

    whoami


Example: syuk

**(1.2)** Also make sure that user has a password set (NoMachine uses system login):

    sudo passwd syuk


**(1.3)** Set/confirm a password.

## **b. Create a new connection in NoMachine (Windows)**

**== On Windows client : ==**

**(1)** Open NoMachine.

**(1)** It may show a “Welcome” screen with detected PCs. If your Jetson/server appears with its Tailscale IP, you can click it directly.

**(1)** If not, do this:

**(2)** Click New to create a new connection.

**(3)** Protocol: choose NX (default).

**(4)** Host: enter your server’s Tailscale IP, e.g.:

    100.64.23.10


**(5)** Port: 4000 (default NoMachine port).

**(6)** Click Next until Finish (you can keep default settings: no proxy, etc.).

**(7)** You now have a connection entry, something like “Connection to 100.64.23.10”.

## **c. Connect to the server via NoMachine**

**(1)** In NoMachine, double-click the connection you just created.

**(2)**First time, it may show a host key fingerprint warning — click Yes / Accept.

**(3)**Then you’ll see a login screen:

    Username: your Linux username (e.g. syuk)

    Password: the password you set or already use for that user

**(4)**After logging in:

    You should see your Linux desktop (or a list of virtual desktops, depending on the environment).

    Choose the default desktop / virtual session if asked.

If everything is correct, you’re now controlling the Jetson/server GUI over Tailscale + NoMachine 😎

## **PART 4 – Common issues & fixes**

A. Can’t connect / timeout in NoMachine

Check:

Tailscale working?

From Windows, ping 100.xx.xx.xx = must reply.

NoMachine running on Linux?

sudo /usr/NX/bin/nxserver --status


If it’s stopped:

sudo /usr/NX/bin/nxserver --startup
sudo /usr/NX/bin/nxserver --restart


Firewall on Linux:

If using ufw:

sudo ufw allow 4000/tcp


If you ping but NoMachine still fails, it’s almost always firewall/port.

B. Black screen / display issues (Linux headless)

If your Jetson/server has no monitor connected, sometimes NoMachine shows black screen.

Try:

Install a dummy X11 driver / virtual screen (depends on your distro).

Or plug a cheap HDMI dummy plug so the GPU thinks there’s a monitor.

C. Use Tailscale hostname instead of IP (optional)

Tailscale gives each device a hostname like jetson-nano.tailnet-name.ts.net.

You can use that instead of IP in NoMachine Host field (sometimes easier to remember).

PART 5 – (Optional) Windows ↔ Windows setup

If both server and client are Windows, steps are almost the same:

Install Tailscale on both → log in with same account.

Install NoMachine on both.

On the client:

Create NoMachine connection with Host = server’s Tailscale IP.

Log in using the Windows username & password on the server PC.

---

## **Screenshot**
