# 🎬 AI Phishing Detector - Video Demo Script

**Duration**: 9-10 minutes  
**Target Audience**: Technical professionals, security teams, AI enthusiasts

---

## 🎯 Video Structure

1. **Hook & Problem** (0:00-1:30)
2. **Solution Overview** (1:30-2:30)
3. **Demo: Orchestrated Workflow** (2:30-5:00)
4. **Demo: MCP Agent** (5:00-7:00)
5. **Results, The Fix, and Discovery** (7:00-9:00)
6. **Call to Action** (9:00-9:30)

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

#### Step 1: What is MCP? (5:00-5:45)

**You**:
> "Now let's look at Version 2 - the MCP Agent. But first, what is MCP?
>
> MCP stands for Model Context Protocol - it's Anthropic's open standard for connecting AI models to external tools and data sources. Think of it like giving Claude a toolbox and letting it decide which tools to use based on the situation.
>
> In traditional automation, YOU decide when to call each tool - like our Version 1 with IF statements. With MCP, the AI decides. You just tell Claude 'here's what these tools do,' and Claude figures out when and how to use them.
>
> It's the same concept behind AutoGPT, LangChain agents, and other autonomous AI systems - but MCP is Anthropic's official, standardized way of doing it."

**[Show workflow comparison]**

**You**:
> "Look at the difference. Version 1 has seven nodes with explicit control flow. Version 2? Just four nodes. That's because Claude is now handling the decision-making internally.
>
> Instead of hardcoded IF statements and multiple Claude nodes, we have ONE AI Agent node with access to tools. Claude decides everything else."

#### Step 2: Show Tool Configuration (5:45-6:15)

**[Click into AI Agent node]**

**You**:
> "Inside the AI Agent, I've given Claude access to one tool: check_virustotal. This is how MCP works - you define tools with descriptions and parameters, and Claude decides when to use them.
>
> Here's my tool description: 'Check if a domain is malicious using VirusTotal threat intelligence. Provide only the domain name.'
>
> Notice what I'm NOT saying: I'm not saying 'IF you find URLs, THEN call this tool.' I'm not giving Claude a flowchart to follow. I'm just saying 'Here's a tool. Use it if you think it's helpful.'
>
> This is the fundamental difference between orchestration and agency. In orchestration, the workflow decides. In MCP, the AI decides.
>
> Claude will read this description, analyze the email, and think: 'I see suspicious URLs - let me check VirusTotal myself.'"

#### Step 3: Execute MCP Workflow (6:15-7:00)

**[Send another test email - different from V1]**

**You**:
> "Let's test it with a different email - this one is a CEO impersonation scam with NO URLs."

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

### PART 4: Results, The Fix, and The Surprising Discovery (7:00-8:45)

**[Screen: Side-by-side comparison of alert emails]**

#### The Initial Problem with V1 (7:00-7:30)

**You**:
> "Before I show you the final results, I need to tell you about a critical bug I discovered in Version 1.
>
> Initially, when I tested both systems, Version 1 had a serious flaw. Watch what happened..."

**[Screen: Show original broken V1 output]**

**You**:
> "This phishing email has clear indicators: urgency tactics, brand impersonation, credential harvesting. Version 1's initial analysis correctly scored it 95 out of 100 - HIGH RISK.
>
> Then VirusTotal checked the domain and returned 'clean' - because it's a legitimate domain registered in 1996.
>
> And look what Version 1 did: it dropped the score from 95 to 25 and recommended 'Allow.'
>
> This is a FALSE NEGATIVE. One of the most dangerous mistakes a security system can make.
>
> The problem? Version 1 was over-trusting VirusTotal. It assumed that if a domain is legitimate, the email must be safe. But that's wrong - legitimate domains can be spoofed, compromised, or used in social engineering attacks."

#### How I Fixed It (7:30-7:50)

**[Screen: Show the updated prompt]**

**You**:
> "I fixed this by updating Claude's prompt in the final analysis step. I added explicit instructions:
>
> 'A clean domain does NOT mean the email is safe. Legitimate domains can be spoofed or compromised. Social engineering tactics remain dangerous regardless of domain reputation. Weigh BOTH factors - don't drastically reduce the score just because VirusTotal is clean.'
>
> This is prompt engineering - being very explicit about how to reason through the problem."

**[Screen: Show fixed V1 output]**

**You**:
> "Now look at Version 1's output after the fix. Same email, same VirusTotal clean result. But now it maintains the 95/100 score and explains:
>
> 'Despite VirusTotal showing the domain as clean, this email remains highly dangerous due to overwhelming social engineering indicators. A clean result does not negate these threats - legitimate domains can be spoofed or compromised.'
>
> Perfect. Version 1 now correctly weighs both factors and maintains the high-risk classification."

#### The MCP Advantage (7:50-8:20)

**[Screen: Show MCP output from the beginning]**

**You**:
> "But here's what's fascinating: the MCP agent NEVER had this problem.
>
> From the very first test, before I fixed anything, the MCP agent correctly handled the clean VirusTotal results. Look at its analysis:
>
> 'This is typosquatting using a .tk free domain commonly abused by attackers. While VirusTotal shows clean, the urgency tactics, credential harvesting attempt, and brand impersonation maintain the critical threat level.'
>
> The MCP agent naturally understood that domain reputation is just ONE factor in phishing detection. It didn't need explicit rules to avoid over-trusting VirusTotal.
>
> This is the power of autonomous reasoning. Version 1 needed me to explicitly program the right behavior through careful prompt engineering. Version 2 figured it out on its own through continuous, contextual thinking."

#### Why MCP is More Accurate (8:20-8:45)

**[Screen: Show detailed MCP analysis]**

**You**:
> "And it's not just about avoiding mistakes. The MCP agent provides significantly better analysis overall.
>
> Look at the depth here:
> - Identifies specific attack techniques: 'typosquatting,' 'Business Email Compromise,' 'advance fee fraud'
> - Explains WHY each indicator matters
> - Provides context: 'BEC attacks cause billions in losses annually'
> - Gives actionable guidance: 'Never process financial requests without proper verification'
>
> Compare that to Version 1, which gives: 'Threat score 95, recommend block, reasoning: multiple phishing indicators detected.'
>
> Both are correct. Both block the threat. But which one would you rather receive at 3 AM when you're on call?
>
> The MCP agent is like having a senior analyst explain the threat to you. Version 1 is like getting an alert from an automated system.
>
> This difference comes down to HOW they think. Version 1's reasoning is fragmented - analyze, check tool, re-analyze. The MCP agent thinks continuously: gather information, synthesize everything, form a complete picture. The result is more coherent, more educational, more useful."

#### Trade-offs and When to Use Each (8:45-9:00)

**[Screen: Comparison table]**

**You**:
> "So after all this testing and fixing, which version should you use? Both are now production-ready and accurate. Here's my recommendation:
>
> **Use Orchestrated Workflow (Version 1) when:**
> - You need predictable, deterministic behavior
> - Debugging and auditability are critical
> - Compliance requires explicit control
> - You want consistent output format
> - You're in a mature SOC with established processes
>
> **Use MCP Agent (Version 2) when:**
> - You want the most detailed threat analysis
> - Your team is learning and needs education
> - You're adding multiple tools and want flexibility
> - You value contextual, adaptive intelligence
> - You want cutting-edge AI agent capabilities
>
> Both systems now achieve 95%+ detection accuracy on the same test set. The difference is HOW they think and WHAT they tell you."

**[Screen: Final statistics]**

**You**:
> "Final numbers:
> - Detection accuracy: 95%+ for both versions
> - False positives: <5%
> - Processing time: 8-15 seconds per email
> - Cost: ~$5 per month in API costs
> 
> Compare that to the average cost of one successful phishing attack: $4.9 million.
>
> This system pays for itself if it catches just one attack."

---

### PART 5: Call to Action (9:00-9:30)

**[Screen: GitHub repository]**

**You**:
> "Both versions of this project are completely open source and ready to deploy. I've included:
> - Full workflow JSON files for both V1 and V2
> - Complete setup instructions with screenshots
> - Sample phishing emails for testing
> - The exact prompts I used, including the fix for V1
> - Documentation explaining every component
>
> Everything is in the GitHub repository linked in the description.
>
> This is a real, production-ready phishing detection system that you can deploy in your organization today. Whether you choose the orchestrated workflow for reliability or the MCP agent for intelligence, you'll have 24/7 automated protection against phishing attacks.
>
> If you want to learn more about building AI agents and automation systems, check out my other videos. I'm building a series on practical AI applications for security, DevOps, and productivity.
>
> Thanks for watching, and remember: the best defense against phishing is a system that never sleeps. Stay secure out there!"

**[End screen with links]**
- GitHub: [Repository Link]
- n8n: n8n.io
- Anthropic: console.anthropic.com
- VirusTotal: virustotal.com

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

### Slide 3: MCP Explained
```
Model Context Protocol (MCP)

Traditional: YOU decide when to call tools
MCP: AI decides when to call tools

🔧 Tools available → 🤖 Claude chooses → ✅ Autonomous agent
```

### Slide 4: The Bug (Before/After)
```
BEFORE (Broken):
Initial: 95/100 HIGH RISK ✅
VT: Clean
Final: 25/100 LOW RISK ❌ FALSE NEGATIVE!

AFTER (Fixed):
Initial: 95/100 HIGH RISK ✅
VT: Clean  
Final: 95/100 HIGH RISK ✅ CORRECT!
```

### Slide 5: Comparison Table
```
| Feature | Orchestrated | MCP Agent |
|---------|-------------|-----------|
| Decision Making | n8n decides | Claude decides |
| Tool Calling | Fixed IF logic | Dynamic |
| Bug Risk | Needed fix | Correct naturally |
| Output Style | Concise | Detailed |
```

### Slide 6: Final Results
```
✅ 95%+ accuracy (both versions after fix)
✅ <5% false positives  
✅ 8-15 sec per email
💰 ~$5/month cost
🛡️ Prevents $4.9M average attack loss
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
2:30 - Demo: Orchestrated Workflow (V1)
5:00 - Demo: MCP Agent (V2)
7:00 - The Critical Bug I Found
7:30 - How I Fixed It
7:50 - Why MCP Didn't Have This Problem
8:20 - Detailed Analysis Comparison
8:45 - Which Version Should You Use?
9:00 - Get the Code & Deploy

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