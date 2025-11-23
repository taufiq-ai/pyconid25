Below is a **clean, professional, PyCon-safe, beginner-friendly** speaker script designed for **~22–24 minutes speaking time + 6–8 minutes Q&A** (total < 30 minutes).
It aligns perfectly with your **accepted proposal on PaperCall** and your slide plan.

You can read this *almost verbatim* on stage.

---

# 🎤 **Full Speaker Script (≈ 23 minutes)**

*(You can trim or expand sections depending on pacing.)*

---

# **Slide 1 — Title**

**“No Cloud? No Problem! Turn Your Phone Into a Remote Linux Server for Python Apps.”**

> **“Hello everyone! Thank you for joining my session.
> My name is Taufiqul Haque Khan Tusar — you can call me Taufiq.
> Today, I’ll show you something a little unusual, something a bit fun, and something extremely practical: how to turn your Android phone into a fully functional remote Linux server for Python apps — no cloud provider required.”**

---

# **Slide 2 — Who Am I?**

> “I work as a Backend & NLP Engineer. I spend most of my time building Django systems, LLM tools, Python-based backends, and automations.
>
> I’m also the founder of the AIML Professional Community Bangladesh where we run workshops and support new developers starting their AI/ML journey.”

---

# **Slide 3 — Sponsor Thanks**

> “A quick thank you to my company for supporting my travel and making this talk possible.
>
> And no, they are not responsible for any questionable ideas I’m about to present… the phone-as-a-server thing is fully my fault.” (smile)

---

# **Slide 4 — The Problem**

> “Let’s start with the why.
>
> Cloud services are powerful, but they’re not always accessible.
> Free tiers are shrinking, paid tiers are expensive, and for many learners — especially students, hobbyists, or people in regions with weaker purchasing power — running even a simple backend can be a financial burden.
>
> And sometimes you just want a small, always-on server for experiments — without deploying to AWS, GCP, Azure, or losing half your savings.”

---

# **Slide 5 — The Idea: Use Your Phone**

> “So the question is: can we repurpose a device we already own?
>
> And the answer is yes: your Android phone *is* a mini computer. It has:
>
> * Multi-core CPU
> * Several gigabytes of RAM
> * Persistent storage
> * A stable IP through Tailscale
> * Ability to run Termux
>
> In other words, it’s a Linux machine you forgot you owned.”

---

# **Slide 6 — Architecture Overview**

*(Show the architecture diagram.)*

> “Here’s the whole setup:
>
> **Phone → Termux → SSH Server → Tailscale → Laptop**
>
> And another branch:
> **Phone → Cloudflare Tunnel → Public HTTPS URL**
>
> Inside the phone, we run:
>
> * Python app
> * Screen to keep it alive
> * Git repo to pull updates
> * Cloudflare Tunnel for access
>
> And UptimeRobot monitors the Cloudflare URL to email us if something stops.
>
> That’s the entire system — no root, no proot-distro, no custom firmware.”

---

# **Slide 7 — Requirements**

> “Here’s what you need:
>
> * Any Android phone (3GB RAM recommended)
> * Termux from F-Droid
> * SSH server inside Termux
> * Tailscale for secure private IP
> * Cloudflare Tunnel for public access
> * Git, Python, and screen
> * And a charger… because we don’t want the server to take a nap.”

---

# **Slide 8 — Step 1: Install Termux**

> “Open Termux and run:
>
> ```bash
> pkg update && pkg upgrade
> pkg install openssh git python screen
> ```
>
> Termux is basically a Linux environment that runs inside Android.
>
> No rooting, no hacks, no risk.”

---

# **Slide 9 — Step 2: Enable SSH & Wake-Lock**

> “Now we turn the phone into an SSH-accessible machine:
>
> ```bash
> sshd
> termux-wake-lock
> ```
>
> Termux runs SSH on port 8022.
>
> Wake-lock prevents Android from killing Termux when the screen is off — very important.”

---

# **Slide 10 — Step 3: Connect Phone & PC via Tailscale**

> “We install Tailscale on the phone and on our laptop:
>
> ```bash
> pkg install tailscale
> tailscale up
> ```
>
> The phone now gets a private IP, for example: `100.x.x.x`.
>
> From the laptop:
>
> ```bash
> ssh -p 8022 u0_a123@100.x.x.x
> ```
>
> Now we’re inside the phone — just like a remote server.”

---

# **Slide 11 — Step 4: Pull Your GitHub Repo**

> “Once inside Termux via SSH, we deploy our Python project:
>
> ```bash
> git clone <repo>
> cd <repo>
> pip install -r requirements.txt
> ```
>
> Nothing special. This is the same workflow you use on any Linux machine.”

---

# **Slide 12 — Step 5: Use `screen` to Keep Server Alive**

> “To ensure the app doesn't stop when the SSH session closes, we use screen:
>
> ```bash
> screen -S server
> python app.py
> ```
>
> Detach with: `Ctrl+A` then `D`.
>
> Reattach with:
>
> ```bash
> screen -r server
> ```
>
> This makes the phone behave like an actual VPS.”

---

# **Slide 13 — Step 6: Make It Public with Cloudflare Tunnel**

> “Tailscale gives us private access, but what if you need a public URL?
>
> Cloudflare Tunnel does exactly that:
>
> ```bash
> pkg install cloudflared
> cloudflared tunnel --url http://localhost:8000
> ```
>
> Cloudflare instantly gives you a secure HTTPS URL — without exposing your phone or forwarding ports.”

---

# **Slide 14 — Step 7: Auto-Restart Script**

> “To make life easier, I use a small script:
>
> ```bash
> #!/data/data/com.termux/files/usr/bin/bash
> screen -dmS myapp bash -c "python app.py"
> cloudflared tunnel --url http://localhost:8000
> ```
>
> This starts everything with one command.
>
> I recommend adding it to Termux:Boot for auto-start.”

---

# **Slide 15 — Step 8: Uptime Monitoring**

> “To make this feel like a real server, we monitor uptime.
>
> UptimeRobot pings the Cloudflare URL and emails us if the phone sleeps, crashes, overheats, or disconnects.
>
> It's surprisingly reliable—much more than you’d expect for a phone server.”

---

# **Slide 16 — Demo Time**

> “Now, here’s a short recorded demo, because unfortunately we don’t have internet here.
>
> I’ll show:
>
> * SSHing into the phone
> * Pulling a repo
> * Starting screen
> * Running the Python app
> * Creating a Cloudflare Tunnel
> * And accessing it live from the browser
>
> All of this running on… an old Android device.”

*(Play video.)*

---

# **Slide 17 — Real Use-Cases**

> “So what can we actually do with this?
>
> * Lightweight Python APIs
> * FastAPI/Flask apps
> * Telegram/Discord bots
> * Periodic scripts
> * Small ML inference models
> * Personal dashboards
> * IoT control panels
> * Web scraping with a stable IP
> * A private development sandbox
>
> It’s not a data center — but it’s incredibly useful.”

---

# **Slide 18 — Limitations**

> “Let’s keep expectations realistic:
>
> ❌ Battery drain
>
> ❌ Heat if you run heavy code
>
> ❌ Limited CPU
>
> ❌ No GPU
>
> ❌ If the phone reboots, you need auto-start scripts
>
> ❌ Not recommended for production
>
> But for learning, prototyping, and lightweight workloads — it’s great.”

---

# **Slide 19 — Tips for Stability**

> “A few tips from my experience:
>
> * Keep the phone plugged in
> * Disable battery optimization for Termux
> * Prefer Wi-Fi over mobile data
> * Use Tailscale ACLs
> * Keep Termux updated
> * Use screen/tmux for persistence
> * Use Termux:Boot for auto-start
> * If possible, use a secondary phone, not your daily driver”

---

# **Slide 20 — Conclusion**

> “To wrap up:
>
> You *can* turn your Android device into a real remote Linux server.
> You *don’t* need paid cloud to learn deployment.
> And this setup is accessible to anyone — everywhere — even with limited hardware or budget.
>
> So the next time someone says they don’t have a server to practice DevOps or Python deployment… tell them to check their pocket.”
> *(smile)*
>
> “Thank you.”

---

# **Slide 21 — Q&A**

> “I’d love to answer your questions.
>
> And if you want the full guide, the scripts, or the diagram, I’ll share everything after the talk.”

---

# ✅ **Done.**

If you'd like, I can also produce:

✅ A shorter 18-minute version
✅ A fully timed script with timestamps
✅ A slide-ready text version
✅ A downloadable PDF
✅ A one-page handout for attendees

Just tell me what you need.
