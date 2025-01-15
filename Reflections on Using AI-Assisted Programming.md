### Reflections on Using AI-Assisted Programming

**Author**: Yao Wang  
**Date**: January 14, 2025  

---

Recently, I’ve been experimenting with AI-assisted programming, spending over 10 hours daily, and here are some of my insights.

The project I worked on is a simple website I developed years ago using PHP and MySQL. It includes a dozen tables and over 10,000 lines of code (including CSS and JavaScript). All the code was handwritten, except for a lesser-known JavaScript library, Mootools, which I used for AJAX calls. I implemented basic page routing, object-relational mapping, and web component reuse in PHP myself.  

### **Purpose of Refactoring**  
The goal of refactoring this website is to separate the frontend and backend, rendering pages entirely with HTML and JavaScript while using PHP only for JSON-formatted AJAX APIs. This approach centralizes UI handling without being constrained by backend language, facilitates future backend language or database switches, and avoids using third-party libraries entirely. The frontend is built with native HTML and JavaScript, while the backend PHP only requires minor updates, primarily to define AJAX APIs, convert database query results into JSON objects, and upgrade syntax from PHP 5 to PHP 8.  

### **Tools Used**  
I used **Windsurf Pro**, which I purchased, and also tried **Cursor**. Windsurf’s chat mode felt more user-friendly, while Cursor had a significant drawback: it couldn’t open files automatically (though it could modify files). This might be a configuration issue on my end. Cursor allows custom AI model setups, while Windsurf only supports GPT-4o, Claude 3.5 Sonnet, and Cascade Base (specific model details are unclear). I chose Sonnet.

### **General Impressions of AI**  
AI behaves like a well-educated junior programmer. It has solid fundamentals and produces clean, best-practice-compliant code and documentation. When given clear instructions, it can implement relatively simple algorithms effectively. It also demonstrates a comprehensive and accurate understanding of programming languages and related fields.  

For example, I opted to use web components for code reuse, a technology I hadn’t used before. AI-generated code sometimes exceeded my knowledge, so I asked it to explain in detail, effectively learning from it. It also created satisfactory SVG-format icons when requested. Additionally, it’s always calm, patient, and willing to explain and revise code repeatedly.

---

### **Challenges**  
However, there are many issues as well:  

1. **Context Limitations**  
   AI often focuses on narrow scopes and fails to consider larger contexts, much like an inexperienced programmer. For instance:  
   - An AJAX call was supposed to return JSON but instead returned an HTML page. AI debugged the backend code multiple times but couldn’t resolve the issue. I manually debugged it and discovered the problem: the JavaScript request lacked the proper `Accept: application/json` header. Once I pointed this out, AI promptly fixed it.  

2. **Debugging and Logical Oversights**  
   In one scenario, a sidebar was supposed to appear, dimming other page elements. However, one element wouldn’t dim. AI debugged it and found that the element had a high `z-index`. It set the element’s `z-index` to 9999 and the overlay to 10000, which solved the issue. But when I asked why the `z-index` was necessary, it admitted I was right and removed it, resolving the problem more cleanly.

   This highlights how AI can sometimes spiral into overly complex solutions, akin to "getting stuck in a mental loop."  

3. **Frequent Code Overwrites**  
   AI would occasionally modify unrelated code, causing unintended issues. While I tried to review changes manually, this wasn’t foolproof.

4. **Instability**  
   Windsurf frequently encountered internal errors and consumed significant CPU and memory resources, often nearing 100%. Given that AI processing occurs server-side, it’s unclear if this is justified.

5. **Incompletion**  
   Even with detailed instructions, AI might only partially complete a task. This could also stem from context limitations.

6. **Credit Usage**  
   Windsurf Pro costs $15/month with 500 prompt credits, with additional credits priced at $10 for 300. Pro Ultimate, offering unlimited credits, costs $60/month. Credits are easily exhausted—100 credits can be used up within a day. I now rely on ChatGPT for knowledge queries and perform simple edits and debugging manually to save credits. Windsurf is primarily used for generating code frameworks, well-defined functions, and complex refactoring.

---

### **Productivity vs. Effort**  
AI-assisted programming significantly boosts productivity, allowing me to work at 10x speed by handling intricate details that traditionally consume most development time. However, due to the aforementioned challenges, I can’t fully rely on AI. I must provide extremely detailed instructions, review code meticulously, offer improvement suggestions, and manually fix bugs when AI malfunctions. This feels like mentoring a junior developer.  

Interestingly, the increased pace leads to greater mental fatigue than traditional development. While AI-assisted programming is often compared to driving an automatic car, it feels more like driving a 10x faster automatic car that frequently malfunctions.

---

### **Future Prospects**  
Will these issues improve with technological advancements? Undoubtedly, stability, context size, code quality, and debugging capabilities will enhance. Eventually, most AI-generated code might no longer require human review—not just because of improved AI quality but because human focus won’t keep up with AI’s productivity.

However, there are two tasks that AI cannot replace (at least for now):  

1. **Defining Requirements**  
   Humans must describe product requirements in detail and without ambiguity. This process is more complex than many assume, as it involves modeling the real world.  

2. **Making Technical Decisions**  
   For example, due to limited resources and long maintenance cycles, I chose native HTML and JavaScript over popular frameworks to minimize future maintenance. Such decisions require technical knowledge, business logic understanding, and even insight into human nature, which current AI lacks.

---

### **Conclusion**  
With these changes, developers’ roles will evolve into hybrid roles combining product manager and technical architect responsibilities, whereas traditional programmer roles will fade out. This is what it ought to be.
