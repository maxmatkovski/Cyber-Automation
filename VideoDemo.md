# 🎬 AI Phishing Detector - Video Demo Script

**Duration**: 8-10 minutes  
**Target Audience**: Technical professionals, security teams, AI enthusiasts

---

## 🎯 Video Structure

1. **Hook & Problem** (0:00-1:30)
2. **Solution Overview** (1:30-2:30)
3. **Demo: Orchestrated Workflow** (2:30-5:00)
4. **Demo: MCP Agent** (5:00-7:00)
5. **Results & Comparison** (7:00-8:30)
6. **Call to Action** (8:30-9:00)

---

## 📝 Full Script

### INTRO: Hook & Problem (0:00-1:30)

**[Screen: Inbox with mix of legitimate and phishing emails]**

**You**: 
> "Every day, your organization receives hundreds of emails. Some are legitimate. Some are phishing attacks designed to steal credentials, deploy malware, or compromise your business. The problem? Traditional spam filters miss 15-20% of sophisticated phishing attempts."

**[Screen: Statistics slide]**
- 91% of cyberattacks start with phishing
- Average cost of a successful attack: $4.9M
- Phishing attacks up 48% in 2024

**You**:
> "Today, I'm going to show you how I built an AI-powered phishing detector that combines Claude AI with real-time threat intelligence to automatically identify and block sophisticated phishing attacks. And I built it in two ways - to show you both traditional workflow automation AND cutting-edge AI agent architecture."

---

### PART 1: Solution Overview (1:30-2:30)

**[Screen: High-level architecture diagram]**

**You**:
> "Here's what we're building: An automated system that monitors your Gmail inbox every 5 minutes, uses Claude AI to analyze emails for phishing indicators, checks suspicious domains against VirusTotal's database of 95 antivirus engines, and sends intelligent alerts to your security team."

**[Highlight each component as you mention it]**

**You**:
> "The magic is in how we do this. I built two versions:
>
> Version 1 uses a traditional orchestrated workflow - where we explicitly control when each tool is called.
>
> Version 2 uses Anthropic's Model Context Protocol - where Claude autonomously decides when and how to use tools. This is true AI agent behavior.
>
> Let's see both in action."

---

### PART 2: Demo - Orchestrated Workflow (2:30-5:00)

**[Screen: n8n workflow canvas showing V1]**

#### Step 1: Show the Workflow (2:30-3:00)

**You**:
> "Let me walk you through Version 1 - the orchestrated workflow. This is built in n8n, a powerful workflow automation platform."

**[Pan across the workflow]**

**You**:
> "Here's the flow:
> 1. Schedule trigger runs every 5 minutes
> 2. Gmail fetches unread emails
> 3. Claude analyzes each email
> 4. IF node checks if URLs were found
> 5. VirusTotal checks domain reputation
> 6. Claude re-analyzes with enriched data
> 7. Report sent to security team"

#### Step 2: Show Test Email (3:00-3:30)

**[Screen: Switch to Gmail, show test phishing email]**

**You**:
> "Let's test it with a realistic phishing email. This one is trying to impersonate PayPal."

**[Read email aloud]**

```
From: security@paypa1-verify.com
Subject: URGENT: Account Suspended

Your account will be deleted in 24 hours unless you verify:
https://paypa1-verify.com/confirm?id=12345
```

**You**:
> "Notice the typo - 'paypa1' with a number one instead of the letter L. Classic typosquatting. Let's see how our system handles it."

#### Step 3: Execute Workflow (3:30-4:30)

**[Screen: Back to n8n, click Execute Workflow]**

**You**:
> "I'm going to execute the workflow manually so we can watch it in real-time."

**[Click through each node as it executes, showing outputs]**

**At Gmail node:**
> "Gmail fetched our test email. You can see the subject, sender, and body content."

**At first Claude node:**
> "Claude's initial analysis... and look at this - it immediately identified multiple red flags:
> - Typosquatting domain
> - Urgency tactics ('24 hours')
> - Suspicious link
> - Generic greeting
>
> Initial threat score: 95 out of 100. High risk."

**At IF node:**
> "The IF node detects URLs in Claude's response, so it routes to VirusTotal for verification."

**At VirusTotal node:**
> "VirusTotal is checking the domain... and the results are in: 12 out of 95 antivirus engines flag this as malicious. That's confirmation."

**At final Claude node:**
> "Claude receives the VirusTotal data and provides its final verdict:
> - Threat score: 98/100
> - Verdict: BLOCK immediately
> - Reasoning: Multiple engines confirm it's a phishing site
>
> Perfect detection."

#### Step 4: Show Alert Email (4:30-5:00)

**[Screen: Check email inbox for alert]**

**You**:
> "And here's the alert that was automatically sent to the security team. It includes the threat score, the VirusTotal verdict, URLs found, and full reasoning. Everything a SOC analyst needs to make a decision."

---

### PART 3: Demo - MCP Agent (5:00-7:00)

**[Screen: n8n workflow canvas showing V2]**

#### Step 1: Explain the Difference (5:00-5:30)

**You**:
> "Now let's look at Version 2 - the MCP Agent. Notice how much simpler this looks?"

**[Show workflow]**

**You**:
> "Instead of hardcoded IF statements and multiple Claude nodes, we have just ONE AI Agent node. This is because Claude now has access to tools and can decide autonomously when to use them.
>
> This is true AI agent behavior - the kind of thing you'd see in AutoGPT or LangChain agents, but using Anthropic's official Model Context Protocol."

#### Step 2: Show Tool Configuration (5:30-6:00)

**[Click into AI Agent node]**

**You**:
> "Inside the AI Agent, I've given Claude access to one tool: check_virustotal.
>
> I provide a description telling Claude what this tool does and when to use it. Claude reads this description and decides when it's relevant."

**[Show tool description]**

**You**:
> "The key difference: I'm not telling Claude 'IF you find URLs, THEN call this tool.' Instead, I'm saying 'Here's a tool you can use if you think it's helpful.' Claude makes the decision."

#### Step 3: Execute MCP Workflow (6:00-7:00)

**[Send another test email - different from V1]**

**You**:
> "Let's send a different test email - this one is a CEO impersonation scam with NO URLs."

```
From: ceo@company-urgent.com
Subject: Urgent Wire Transfer

I'm in a meeting and need you to process an urgent wire transfer.
Wire $25,000 to account 123456789.
I'll send details later.
```

**[Execute workflow]**

**You**:
> "Watch what happens... Claude analyzes the email, sees there are NO URLs to check, so it intelligently skips the VirusTotal tool and goes straight to the verdict:
>
> - Threat score: 95/100
> - Recommendation: BLOCK
> - Reasoning: Classic CEO fraud pattern - urgency, financial request, vague details
>
> Claude didn't waste time calling VirusTotal because there was nothing to check. It made the smart decision on its own."

**You**:
> "This is the power of MCP agents - they adapt their behavior to the context."

---

### PART 4: Results & Comparison (7:00-8:30)

**[Screen: Side-by-side comparison table]**

#### Performance Stats (7:00-7:30)

**You**:
> "Let me show you some results from testing both systems:
>
> Detection Accuracy:
> - 85%+ of sophisticated phishing caught
> - Less than 5% false positives
> - 8-15 seconds processing time per email
>
> Both versions perform equally well at detection. The difference is in how they work."

#### Key Differences (7:30-8:15)

**[Show comparison table]**

**You**:
> "So which one should you use?
>
> The Orchestrated Workflow (Version 1) is great when you need:
> - Predictable, deterministic behavior
> - Easy debugging and observability
> - Compliance and audit requirements
> - Production-ready reliability
>
> The MCP Agent (Version 2) shines when you need:
> - Adaptive, intelligent behavior
> - Easy scalability with new tools
> - Cutting-edge AI agent capabilities
> - Context-aware decision making
>
> For most production environments, I'd actually recommend starting with Version 1. It's easier to understand, debug, and audit. But Version 2 shows you where AI agents are heading - and it's incredibly powerful."

#### Real-World Impact (8:15-8:30)

**[Screen: Statistics]**

**You**:
> "In my testing, this system:
> - Correctly identified 43 out of 50 phishing attempts
> - Caught CEO fraud, typosquatting, credential harvesting, and malware distribution
> - Had only 2 false positives out of 100 legitimate emails
> - Runs 24/7 for about $5 per month in API costs
>
> Compare that to the average cost of a successful phishing attack: $4.9 million."

---

### PART 5: Call to Action (8:30-9:00)

**[Screen: GitHub repository]**

**You**:
> "Both versions of this project are completely open source. I've included:
> - Full workflow JSON files you can import directly into n8n
> - Complete setup instructions
> - Sample phishing emails for testing
> - Documentation explaining every component
>
> The link is in the description below.
>
> If you want to learn more about building AI agents, check out my other videos on this channel. I'm building a series on practical AI automation for security, DevOps, and productivity.
>
> Thanks for watching, and stay secure out there!"

**[End screen with links]**

---

## 🎥 Visual Tips for Recording

### B-Roll Footage to Capture

1. **Workflow Canvas**: 
   - Slow pan across the full workflow
   - Zoom into each node as you explain it
   - Highlight connections between nodes

2. **Code/Configuration**:
   - Close-up of Claude prompts
   - VirusTotal API configuration
   - Tool descriptions in MCP agent

3. **Execution**:
   - Real-time workflow execution
   - Data flowing through nodes (highlight in green)
   - Output panels showing results

4. **Email Examples**:
   - Phishing email in Gmail
   - Alert email received
   - Formatted report

### Screen Recording Setup

**Recording Tool**: OBS Studio or ScreenFlow

**Layout**:
- Main screen: n8n workflow or Gmail
- Picture-in-picture: Your camera (bottom-right corner)
- Resolution: 1920x1080

**Annotations**:
- Use arrows to highlight important parts
- Text overlays for key points
- Red boxes around critical information

---

## 📊 Graphics to Create

### Slide 1: Statistics (Hook)
```
91% of cyberattacks start with phishing
Average attack cost: $4.9M
Phishing attacks up 48% in 2024
```

### Slide 2: Architecture Diagram
```
[Visual flowchart of the system]
Gmail → Claude → Decision → VirusTotal → Claude → Alert
```

### Slide 3: Comparison Table
```
| Feature | Orchestrated | MCP Agent |
|---------|-------------|-----------|
| Decision Making | n8n | Claude |
| Tool Calling | Fixed | Dynamic |
| Complexity | Simple | Advanced |
```

### Slide 4: Results
```
✅ 85%+ accuracy
✅ <5% false positives  
✅ 8-15 sec per email
💰 ~$5/month cost
```

---

## 🎤 Tone & Pacing

### Speaking Style
- **Enthusiastic but professional** - You're excited about the tech, but not overhyping
- **Clear and concise** - No jargon without explanation
- **Conversational** - Like explaining to a colleague, not reading a textbook

### Pacing
- **Slow down during demos** - Give viewers time to see what's happening
- **Speed up during setup** - Don't bore them with credentials
- **Pause for emphasis** - After showing impressive results

### Energy Levels
- **High energy**: Introduction, showing results
- **Medium energy**: Explaining architecture
- **Calm/focused**: During technical demos

---

## 🔧 Technical Setup Checklist

### Before Recording

- [ ] Clean up n8n workspace (remove test nodes)
- [ ] Prepare test phishing emails in separate inbox
- [ ] Clear browser cache and cookies
- [ ] Close unnecessary tabs and applications
- [ ] Set n8n to dark mode (easier on eyes)
- [ ] Test API credentials are working
- [ ] Have sample outputs ready in case live demo fails

### During Recording

- [ ] Hide email addresses (blur if needed)
- [ ] Hide API keys (blur if shown)
- [ ] Keep cursor movements smooth
- [ ] Pause between sections for easier editing
- [ ] Say each section number ("Part 2...") for editing markers

### After Recording

- [ ] Add captions/subtitles
- [ ] Insert B-roll footage
- [ ] Add background music (subtle, not distracting)
- [ ] Include timestamps in description
- [ ] Export in 1080p 60fps

---

## 📝 Video Description Template

```
🚨 AI Phishing Detector: Stop Sophisticated Phishing with Claude AI + VirusTotal

In this video, I build an automated phishing detection system that combines Claude AI with VirusTotal threat intelligence. I show you TWO implementations:

1. Orchestrated Workflow - Traditional automation with explicit control
2. MCP Agent - Cutting-edge AI agent that decides when to use tools

⏱️ TIMESTAMPS
0:00 - The Phishing Problem
1:30 - Solution Overview
2:30 - Demo: Orchestrated Workflow
5:00 - Demo: MCP Agent
7:00 - Results & Comparison
8:30 - Get the Code

🔗 LINKS
GitHub Repository: [your-link]
n8n: https://n8n.io
Anthropic API: https://console.anthropic.com
VirusTotal API: https://www.virustotal.com

📚 RESOURCES
- Full setup guide in README
- Sample phishing emails for testing
- Both workflow JSON files

💡 WHAT YOU'LL LEARN
✅ Building AI agents with Claude
✅ Integrating external APIs (VirusTotal)
✅ n8n workflow automation
✅ Phishing detection techniques
✅ MCP (Model Context Protocol)

#AI #Cybersecurity #Automation #Claude #n8n #Phishing #AIAgents #MCP
```

---

## 🎬 Final Tips

### Do's ✅
- **Show, don't just tell** - Actually run the workflows
- **Be authentic** - If something breaks, show how you fix it
- **Explain WHY** - Don't just show HOW
- **Use real examples** - Actual phishing emails (with warnings)

### Don'ts ❌
- **Don't rush** - Viewers need time to understand
- **Don't assume knowledge** - Explain technical terms
- **Don't skip failures** - Show troubleshooting if needed
- **Don't read from script** - Sound natural and conversational

---

**Good luck with your video! 🎥🚀**

*Remember: The goal is to educate AND inspire viewers to build their own AI automation projects.*