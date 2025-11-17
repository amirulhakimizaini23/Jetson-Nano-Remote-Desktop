# **Jetson Nano Remote Desktop**

This is a repository containing a jetson nano remote desktop using different network

---

## **Description**

Install Tailscale on the Jetson Nano and on your laptop. Once both devices are connected to Tailscale, they appear in the same private network. Use the Jetson Nano’s Tailscale IP (100.x.x.x) in NoMachine. NoMachine connects through Tailscale, giving you secure remote desktop access from anywhere in the world.

---

## **Table Of Content**

- [Tailscale](#tailscale)
- [Nomachine](#nomachine)
- [Simulator](#simulator)
- [Dashboard](#dashboard)
- [Design](#design)

---

## **Tailscale**

**How to Install Tailscale on Windows (Step-by-Step)**

**1. Download Tailscale**

**a.** Open your browser and go to:
https://tailscale.com/download

**b.** Under Windows, click Download for Windows.

**c.** Save the installer file (e.g., Tailscale-Setup.exe).

**2. Install Tailscale**

**a.** Double-click the downloaded Tailscale-Setup.exe.

**b.** Click Yes if Windows asks permission to install.

**c.** Follow the installer prompts:

  **@** Click Next

  **@** Accept licence terms

  **@** Click Install

**d.** The installation normally takes less than 10 seconds.

**3. Start Tailscale**

**a.** After installation, Tailscale will start automatically.

**b.** If not, open it from:
Start Menu → Tailscale

**4. Log In to Your Tailscale Account**

A browser window will appear asking you to log in.

Choose your login method:

Google

Microsoft

GitHub

Email (Magic Link)

Click Allow to authorize your Windows device.

**5. Connect to the Tailscale Network**

Once logged in:

Tailscale will automatically connect.

You will see Connected in the tray icon.

Your device will now receive a Tailscale IP like:

100.xx.xx.xx

6. Optional: Enable “Run at Startup”

Click the Tailscale icon in the taskbar.

Click Preferences.

Check Start Tailscale when Windows starts.

7. (Optional) Set as “Exit Node” or Use One

You can:

Use another device’s internet connection
or

Make your Windows PC an exit node.

To enable exit node (sharing your internet):

Open Tailscale

Go to Settings

Enable Advertise exit node

To use an exit node:

Open Tailscale

Select your preferred exit node under Route Settings

---

## **Nomachine**
