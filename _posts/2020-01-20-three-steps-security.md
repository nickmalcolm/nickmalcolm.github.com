---
title: "Three easy steps for securing your next project"
excerpt_separator: <!--more-->
---

_This post was first published on [aurainfosec.com](https://www.aurainfosec.com/news-and-events/files/three-easy-steps-for-securing-your-next-project.html)._


Technology managers and business owners understand that they are kaitiaki, or guardians, of their organisation and customer data and that they must take steps to safeguard it. This responsibility is heightened during projects which change the way we interact with or store data – whether it’s creating a new website on AWS, lifting-and-shifting a legacy application to Azure, or switching from on-premise office to Office365. There is a perception that security is hard or requires expertise, so it’s easier to ignore it until the end of the project, but this line of thinking is letting the perfect be the enemy of the good. There can be a middle ground!

There are three straightforward teams can take to deliver a secure solution that your customers can trust. First, think about what could go wrong; second, leverage the tools, frameworks, and knowledge which already exists; and third, verify before go-live.

<!--more-->

## Step 1. Collaboratively identify potential problem areas.

Early in the project, gather a cross-section of the project team for a workshop – the more diverse the audience, the better. Using a wall or whiteboard and post-it notes, draw a vertical line where <em>Low Impact</em> is at the bottom and <em>High Impact</em> is at the top, and a horizontal line where is <em>Low Likelihood</em> is on the left <em>and High Likelihood</em> is on the right (like an X-Y graph). Brainstorm as a team what could go wrong and how, then as a group position notes on the wall based on how likely or severe those risks are.

Your team now has a visual representation and a shared understanding of what risks matter the most: the post-its in the top right quadrant. Well-described risks will describe both a cause and an effect – this makes them easier to address.

Capture these risks so the team can refer to them and work on addressing these throughout the project. You could add controls to reduce the likelihood (e.g. <em>we will do peer code reviews before making firewall changes</em>) or reduce the impact (e.g. <em>we will encrypt customer data at rest, so that even if the firewall is misconfigured the attacker can’t read the data</em>). Another approach is avoiding risk, usually by redesigning aspects of the solution.

You can find more step-by-step details on running a workshop like this by reading <a href="https://www.atlassian.com/team-playbook/plays/pre-mortem">“Atlassian Team Playbook: Premortem”</a> or <a href="https://www.doteveryone.org.uk/project/consequence-scanning/">DotEveryone’s “Consequence Scanning”</a>.

## Step 2. Leverage existing frameworks and tools

While almost every project delivers something uniquely valuable, we typically build on a foundation of common software and platforms. The same is true of security – there are foundational frameworks and tools which can be leveraged to help build in security from the start.

If you’re using Azure, check out their <a href="https://docs.microsoft.com/en-us/azure/security/fundamentals/technical-capabilities#secure-your-application">Security Fundamentals</a> series and run through <a href="https://docs.microsoft.com/en-us/azure/security/fundamentals/operational-checklist">Azure’s Security Checklist</a>. Use <a href="https://docs.microsoft.com/en-us/azure/advisor/index">Azure Advisor</a> throughout the project to ensure everything is configured securely.

If you’re using AWS, read through their <a href="https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf">Security Best Practices whitepaper</a>. Use <a href="https://aws.amazon.com/premiumsupport/technology/trusted-advisor/">AWS Trusted Advisor</a> so any security issues are highlighted to the team.

Finally, check out OWASP’s <a href="https://www.owasp.org/index.php/OWASP_Proactive_Controls">Top 10 Proactive Controls</a>. These are a set of security requirements and techniques which should be considered in any software project.

## Step 3. Verify before Go-Live

You’ve identified risks at the start of the project and leveraged secure foundations through the build phase. Now we need to make sure we’re good to go.

Revisit those top risks. Have we reduced the chances of them happening? Have we limited the impact if it were to happen? When doing our acceptance testing, have we tried to impersonate a hacker and misuse the application (testing the “negative path”)? Have we sat around a table and practiced how would we respond to an incident? Have we clearly outlined and communicated roles and responsibilities for maintenance going forward?

Look again at the Trusted Advisor tools. Are there any outstanding issues? Is all our software up to date? Is administrative access configured with strong passwords and multi-factor authentication?

If your solution is business-critical, or if the team identified more than a handful of noteworthy risks, bring in some outside help. An independent party with expertise in identifying security issues can give assurance that the solution has been built securely and risks have been addressed.

When faced with a myriad of potential security activities on the ‘to do’ list, fulfilling our obligation to safeguard systems and data can feel like a daunting task. But by starting with the three steps above, you and your team will be well placed to deliver a secure, responsible solution.
</div>