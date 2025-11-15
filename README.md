# Project Overview--->Vanguard-Planner-Agent 

This project brings to life Agent Shutton—a smart, multi-agent system created to help users craft diverse blog posts with ease. Built using Google’s Agent Development Kit (ADK), it uses a flexible, modular design that lets the agent coordinate specialized tasks smoothly, resulting in high-quality, customized content. By combining the strengths of advanced Google tools and a clean architecture, Agent Shutton makes blog writing more creative, efficient, and accessible for everyone.​
![Uploading generated-image (13).png…]()

### Problem Statement.
Writing blogs by hand can take a lot more energy than it seems at first. Each post requires hours of research, outlining, drafting, editing, and formatting, and starting from scratch every time can quickly wear you down. Trying to keep the structure consistent and the tone steady across multiple articles only adds to the mental fatigue. As content needs grow, manual writing becomes even harder to scale, forcing creators to choose between producing fewer posts or sacrificing quality — unless they hire additional help. Automation can ease much of this burden by gathering research, creating first drafts, keeping formatting consistent, and managing publishing schedules. This frees writers to spend their time on strategy, creativity, and the kind of insight that truly requires a human touch.

### Solution Statement
Agents can take over the research process by pulling information from different sources, summarizing the most important points, and spotting trends that matter to your audience. They can also create draft outlines or even full articles based on the tone, length, and style you choose, which helps eliminate the stress of facing a blank page. Beyond writing, agents can handle the entire publishing workflow—scheduling posts, sharing content across platforms, tracking performance, and offering suggestions based on engagement. This turns blog management from a time-consuming manual task into a smooth, data-driven system.

### Architecture

Core to Agent Shutton is the `Vanguard-Planner-Agent` -- a prime example of a multi-agent system. It's not a monolithic application but an ecosystem of specialized agents, each contributing to a different stage of the blog creation process. This modular approach, facilitated by Google's Agent Development Kit, allows for a sophisticated and robust workflow. The central orchestrator of this system is the `interactive_Vanguard-Planner-Agent`.
![Architecture](./flow_adk_web.png "Optional Title")

The `interactive_Vanguard-Planner-Agent` is constructed using the `Agent` class from the Google ADK. Its definition highlights several key parameters: the `name`, the `model` it uses for its reasoning capabilities, and a detailed `description` and `instruction` set that governs its behavior. Crucially, it also defines the `sub_agents` it can delegate tasks to and the `tools` it has at its disposal.
The real power of the `Vanguard-Planner-Agent` lies in its team of specialized sub-agents, each an expert in its domain.

**Content Strategist:
This agent’s job is to build a clear, well-organized outline for the blog post. When a codebase is included, it automatically adds sections for code snippets and deeper technical explanations. To keep the quality high, the agent is designed as a LoopAgent, which means it can retry and refine its work until it meets the right standards. The OutlineValidationChecker makes sure the outline follows the required guidelines before moving forward.

**Technical Writer:
Once the outline is approved, the robust_blog_writer steps in. This agent acts like a skilled technical writer, creating detailed and engaging articles tailored for a knowledgeable audience. It uses the finalized outline and the codebase summary to build the post, focusing on clear explanations and helpful code examples. Just like the planner, it operates as a LoopAgent, relying on a BlogPostValidationChecker to make sure the content meets the expected quality before moving forward.

### Essential Tools and Utilities

The `Vanguard-Planner-Agent` and its sub-agents are equipped with a variety of tools to perform their tasks effectively.

**File Saving (`save_blog_post_to_file`)**

A simple yet essential tool that allows the `Vanguard-Planner-Agent` to export the final blog post to a Markdown file.

**Validation Checkers (`OutlineValidationChecker`, `BlogPostValidationChecker`)**

These custom `BaseAgent` implementations are a key part of the system's robustness. They check for the presence and validity of the blog outline and post, respectively. If the validation fails, they do nothing, causing the `LoopAgent` to retry. If the validation succeeds, they escalate with `EventActions(escalate=True)`, which signals to the `LoopAgent` that it can proceed. This is a powerful mechanism for ensuring quality and controlling the flow of execution in a multi-agent system.

### Conclusion
The strength of the Vanguard-Planner-Agent comes from its iterative, collaborative workflow. The interactiveVanguard-Planner-Agent works like a project manager, coordinating the different specialists on the team. It assigns tasks, collects user feedback, and makes sure every step of the content creation process is completed smoothly. Thanks to the Google ADK, this multi-agent setup is modular, reusable, and easy to scale.

The Vanguard-Planner-Agent shows how effective multi-agent systems can be when built with a powerful framework like Google’s Agent Development Kit. By breaking the technical writing process into smaller, focused tasks and letting dedicated agents handle each one, it creates a workflow that’s both efficient and reliable.

### Value Statement

Agent Shutton reduced my blog development time by 6-8 hours per week, enabling me to produce more content at higher quality. I have also been producing blogs across new domains - as the agent drives research that I'd otherwise not be able to do given time constraints and subject matter expertise.

If I had more time I would add an additional agent to scan various sites for trending topics and use that research to inform my blog topics. This would require integrating applicable MCP servers or building custom tools. 

## Installation

This project was built against Python 3.11.3.

It is suggested you create a vitrual environment using your preferred tooling e.g. uv.

Install dependenies e.g. pip install -r requirements.txt

### Running the Agent in ADK Web mode

From the command line of the working directory execute the following command. 

```bash
adk web
```

**Run the integration test:**

```bash
python -m tests.test_agent
```



