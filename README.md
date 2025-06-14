<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ahmed Achbarou | Full-Stack Developer</title>
    <!-- Chosen Palette: Digital Night -->
    <!-- Application Structure Plan: This final version enhances the two-column layout by adding a dedicated "Services" section and rewriting project descriptions to be impact-focused. This provides a clearer value proposition for potential clients and recruiters. The navigation and interactive terminal have been updated to reflect these content additions, creating a more comprehensive and professional narrative. Gemini API features have been added to the terminal and project cards. -->
    <!-- Visualization & Content Choices: 
        - The "Services" section uses a clean card layout, which is highly readable and standard for presenting core competencies.
        - Project descriptions were rewritten from feature-based to results-based to better communicate professional value.
        - The interactive terminal's command list was expanded to include a new `ask` command powered by the Gemini API.
        - Project cards now feature an "AI README" generator, also powered by Gemini, to showcase practical AI integration.
        - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. 
    -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600&family=Inter:wght@400;500;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0D1117;
            color: #C9D1D9;
        }
        html {
            scroll-behavior: smooth;
        }
        .font-mono {
            font-family: 'Fira Code', monospace;
        }
        .text-accent { color: #39D353; } /* A vibrant green accent */
        .bg-accent { background-color: #39D353; }
        .bg-accent-hover:hover { background-color: #39D353; }
        .text-accent-hover:hover { color: #39D353; }
        
        .bg-card { background-color: #161B22; }
        .border-card { border-color: #30363D; }
        
        #matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            filter: blur(2px);
        }

        .nav-link.active {
            color: #39D353;
            font-weight: 600;
        }
        .nav-link.active::before {
            content: '$ ';
            animation: blink-cursor 1s step-end infinite;
        }
        
        @keyframes blink-cursor {
          50% { opacity: 0; }
        }
        
        .project-card, .timeline-item, .service-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .project-card:hover, .service-card:hover {
             transform: translateY(-5px);
             box-shadow: 0 0 15px rgba(57, 211, 83, 0.2);
        }
        
        .fade-in-section {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }

        .fade-in-section.is-visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        /* Skills Matrix Styles */
        .skill-tab {
            transition: background-color 0.2s, color 0.2s;
        }
        .skill-tab.active {
            background-color: #39D353;
            color: #0D1117;
        }
        .skill-content {
            display: none;
        }
        .skill-content.active {
            display: block;
        }
        .skill-bar-bg {
            background-color: #30363D;
        }
        .skill-bar-fill {
            background-color: #39D353;
            transition: width 0.8s ease-out;
        }
        
        /* Terminal Styles */
        #terminal {
            background-color: rgba(1, 4, 9, 0.9);
            border: 1px solid #30363D;
            border-radius: 8px;
            height: 450px;
            padding: 1rem;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        #terminal-output { flex-grow: 1; overflow-y: auto; font-family: 'Fira Code', monospace; font-size: 0.9rem; line-height: 1.6; }
        #terminal-output::-webkit-scrollbar { width: 6px; }
        #terminal-output::-webkit-scrollbar-track { background: #010409; }
        #terminal-output::-webkit-scrollbar-thumb { background: #30363D; }
        .terminal-line { white-space: pre-wrap; }
        .terminal-input-line { display: flex; align-items: center; }
        #terminal-input { background: transparent; border: none; outline: none; color: #C9D1D9; flex-grow: 1; font-family: 'Fira Code', monospace; font-size: 0.9rem; }
        #cursor { background-color: #39D353; width: 8px; height: 1.2em; display: inline-block; animation: blink-cursor 1s step-end infinite; }

        /* Modal Styles */
        #modal-backdrop {
            transition: opacity 0.3s ease;
        }
        #modal-content {
            transition: transform 0.3s ease, opacity 0.3s ease;
        }
    </style>
</head>
<body class="antialiased">
    
    <canvas id="matrix-bg"></canvas>

    <div class="relative z-10 flex flex-col md:flex-row min-h-screen">
        <!-- Left Fixed Column -->
        <aside class="w-full md:w-1/3 lg:w-1/4 xl:w-1/5 p-8 md:p-10 bg-card/80 backdrop-blur-md md:h-screen md:sticky md:top-0 flex flex-col justify-between border-r border-card">
            <div>
                <div class="text-center md:text-left mb-8">
                    <img src="https://placehold.co/200x200/161B22/39D353?text=AA" alt="Ahmed Achbarou" class="w-32 h-32 rounded-full mx-auto md:mx-0 mb-6 border-4 border-accent shadow-lg">
                    <h1 class="text-3xl font-bold text-white">Ahmed Achbarou</h1>
                    <p id="typing-subtitle" class="text-accent font-mono mt-1 h-6"></p>
                </div>
                <nav id="desktop-nav" class="space-y-4">
                    <a href="#about" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">About</a>
                    <a href="#services" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">Services</a>
                    <a href="#skills" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">Skills</a>
                    <a href="#projects" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">Projects</a>
                    <a href="#terminal-section" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">Terminal</a>
                    <a href="#contact" class="nav-link block font-medium text-lg text-gray-400 text-accent-hover transition-colors duration-200">Contact</a>
                </nav>
            </div>
            <div class="mt-12 text-center md:text-left">
                <div class="flex justify-center md:justify-start space-x-4">
                    <a href="https://github.com/aachbarou" target="_blank" class="text-gray-400 text-accent-hover"><span class="font-mono text-2xl">GH</span></a>
                    <a href="https://linkedin.com/in/ahmed-achbarou" target="_blank" class="text-gray-400 text-accent-hover"><span class="font-mono text-2xl">LI</span></a>
                </div>
                 <p class="text-xs text-gray-500 mt-4">&copy; 2025 Ahmed Achbarou</p>
            </div>
        </aside>

        <!-- Right Scrollable Column -->
        <main class="w-full md:w-2/3 lg:w-3/4 xl:w-4/5 p-8 md:p-12 lg:p-16">
            <section id="about" class="min-h-screen flex items-center fade-in-section">
                <div>
                    <p class="font-mono text-accent mb-4">./README.md</p>
                    <h2 class="text-4xl lg:text-5xl font-extrabold text-white mb-6">Problem Solver, Code Crafter, Technology Enthusiast.</h2>
                    <div class="space-y-4 text-lg text-gray-400 max-w-3xl">
                        <p>I build robust, scalable web solutions with a focus on clean architecture and performance. Specializing in <strong class="text-white">Go</strong> for powerful backends and <strong class="text-white">React</strong> for dynamic frontends, I enjoy the entire development lifecycle, from ideation to deployment.</p>
                        <p>Based in Morocco, I'm constantly exploring new technologies to push the boundaries of what's possible on the web.</p>
                    </div>
                    <div class="mt-12">
                        <h3 class="font-mono text-lg text-white mb-4">Education & Milestones</h3>
                        <div class="border-l-2 border-card pl-6 space-y-8">
                            <div class="timeline-item relative"><div class="absolute -left-[34px] top-1 h-4 w-4 rounded-full bg-accent"></div><p class="font-mono text-accent text-sm">2022 - Present</p><h4 class="text-white font-semibold text-xl">Freelance Developer</h4><p class="text-gray-400">Delivering full-stack solutions for clients worldwide.</p></div>
                            <div class="timeline-item relative"><div class="absolute -left-[34px] top-1 h-4 w-4 rounded-full bg-accent"></div><p class="font-mono text-accent text-sm">Zone 01 Tech Hub</p><h4 class="text-white font-semibold text-xl">Specialized IT & Software Development Training</h4><p class="text-gray-400">Intensive, project-based training focused on backend systems with Go and Node.js, improving system performance and stability.</p></div>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="services" class="py-20 fade-in-section">
                <p class="font-mono text-accent mb-4">./services --list</p>
                <h2 class="text-4xl font-bold text-white mb-12">What I Do</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="service-card bg-card border border-card rounded-lg p-6">
                        <h3 class="text-xl font-bold text-white mb-3 font-mono">[ Backend Development ]</h3>
                        <p class="text-gray-400">Building secure, scalable, and high-performance APIs and microservices using Go and Node.js.</p>
                    </div>
                    <div class="service-card bg-card border border-card rounded-lg p-6">
                        <h3 class="text-xl font-bold text-white mb-3 font-mono">[ Frontend Development ]</h3>
                        <p class="text-gray-400">Crafting responsive and interactive user interfaces with modern frameworks like React.</p>
                    </div>
                    <div class="service-card bg-card border border-card rounded-lg p-6">
                        <h3 class="text-xl font-bold text-white mb-3 font-mono">[ Full-Stack Solutions ]</h3>
                        <p class="text-gray-400">Leading projects from concept to deployment, ensuring a cohesive and robust final product.</p>
                    </div>
                </div>
            </section>

            <section id="skills" class="py-20 fade-in-section">
                 <p class="font-mono text-accent mb-4">./skills --list</p>
                 <h2 class="text-4xl font-bold text-white mb-12">Skills Matrix</h2>
                 <div class="w-full max-w-4xl mx-auto">
                    <div class="flex flex-wrap gap-2 border-b border-card mb-6">
                        <button class="skill-tab active font-mono py-2 px-4 rounded-t-lg" data-tab="backend">Backend</button>
                        <button class="skill-tab font-mono py-2 px-4 rounded-t-lg" data-tab="frontend">Frontend</button>
                        <button class="skill-tab font-mono py-2 px-4 rounded-t-lg" data-tab="databases">Databases</button>
                        <button class="skill-tab font-mono py-2 px-4 rounded-t-lg" data-tab="tools">Tools & DevOps</button>
                    </div>
                    <div id="skills-content" class="space-y-6">
                        <div id="backend" class="skill-content active space-y-4">
                            <div><p class="mb-1">Go (Golang)</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 90%;"></div></div></div>
                            <div><p class="mb-1">Node.js</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 80%;"></div></div></div>
                            <div><p class="mb-1">PHP</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 60%;"></div></div></div>
                        </div>
                         <div id="frontend" class="skill-content space-y-4">
                            <div><p class="mb-1">React</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 85%;"></div></div></div>
                            <div><p class="mb-1">JavaScript (ES6+)</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 90%;"></div></div></div>
                            <div><p class="mb-1">HTML5 & CSS3</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 95%;"></div></div></div>
                        </div>
                        <div id="databases" class="skill-content space-y-4">
                             <div><p class="mb-1">PostgreSQL</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 75%;"></div></div></div>
                            <div><p class="mb-1">MySQL</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 80%;"></div></div></div>
                            <div><p class="mb-1">SQLite</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 70%;"></div></div></div>
                        </div>
                        <div id="tools" class="skill-content space-y-4">
                            <div><p class="mb-1">Docker</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 70%;"></div></div></div>
                            <div><p class="mb-1">Git & GitHub</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 95%;"></div></div></div>
                            <div><p class="mb-1">Linux</p><div class="skill-bar-bg w-full rounded-full h-2.5"><div class="skill-bar-fill h-2.5 rounded-full" style="width: 85%;"></div></div></div>
                        </div>
                    </div>
                 </div>
            </section>

            <section id="projects" class="py-20 fade-in-section">
                 <p class="font-mono text-accent mb-4">ls -l ./projects</p>
                 <h2 class="text-4xl font-bold text-white mb-8">Featured Projects</h2>
                 <div id="project-filters" class="flex flex-wrap gap-3 mb-8">
                     <button class="filter-btn active bg-accent text-black py-2 px-4 rounded-full text-sm font-semibold" data-filter="all">All</button>
                     <button class="filter-btn bg-card bg-accent-hover text-white py-2 px-4 rounded-full text-sm font-semibold" data-filter="go">Go</button>
                     <button class="filter-btn bg-card bg-accent-hover text-white py-2 px-4 rounded-full text-sm font-semibold" data-filter="react">React</button>
                     <button class="filter-btn bg-card bg-accent-hover text-white py-2 px-4 rounded-full text-sm font-semibold" data-filter="node">Node.js</button>
                 </div>
                 <div id="project-grid" class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="project-card bg-card border border-card rounded-lg p-6 flex flex-col" data-tags="go">
                        <h3 class="text-xl font-bold text-white mb-2">Ecommerce Platform</h3><p class="text-gray-400 mb-4 flex-grow">Engineered a high-performance backend using Go to handle high traffic, resulting in a 50% faster API response time.</p>
                        <div class="font-mono text-xs text-accent mb-4">#Go #PostgreSQL #REST_API</div>
                        <button class="ai-readme-btn mt-auto text-sm font-semibold text-accent text-left">✨ AI README</button>
                    </div>
                    <div class="project-card bg-card border border-card rounded-lg p-6 flex flex-col" data-tags="react,node">
                        <h3 class="text-xl font-bold text-white mb-2">Social Network App</h3><p class="text-gray-400 mb-4 flex-grow">Developed a full-stack social app supporting real-time chat for over 1,000 concurrent users with sub-100ms latency.</p>
                        <div class="font-mono text-xs text-accent mb-4">#React #Node.js #WebSocket</div>
                        <button class="ai-readme-btn mt-auto text-sm font-semibold text-accent text-left">✨ AI README</button>
                    </div>
                    <div class="project-card bg-card border border-card rounded-lg p-6 flex flex-col" data-tags="react,go">
                        <h3 class="text-xl font-bold text-white mb-2">Analytics Dashboard</h3><p class="text-gray-400 mb-4 flex-grow">Created a responsive data visualization dashboard that increased data accessibility for business stakeholders by 40%.</p>
                        <div class="font-mono text-xs text-accent mb-4">#React #Go #Data_Viz</div>
                        <button class="ai-readme-btn mt-auto text-sm font-semibold text-accent text-left">✨ AI README</button>
                    </div>
                    <div class="project-card bg-card border border-card rounded-lg p-6 flex flex-col" data-tags="node">
                        <h3 class="text-xl font-bold text-white mb-2">Real-time Chat API</h3><p class="text-gray-400 mb-4 flex-grow">Architected a scalable WebSocket service with Node.js to handle thousands of simultaneous connections for a live chat feature.</p>
                        <div class="font-mono text-xs text-accent mb-4">#Node.js #Express #Socket.IO</div>
                        <button class="ai-readme-btn mt-auto text-sm font-semibold text-accent text-left">✨ AI README</button>
                    </div>
                 </div>
            </section>
            
            <section id="terminal-section" class="py-20 fade-in-section">
                <p class="font-mono text-accent mb-4">./start_session</p>
                <h2 class="text-4xl font-bold text-white mb-8">Interactive Terminal</h2>
                <div id="terminal">
                    <div id="terminal-output"></div>
                    <div class="terminal-input-line">
                        <span class="text-accent font-mono">$</span>
                        <input type="text" id="terminal-input" autocomplete="off" autofocus>
                        <span id="cursor"></span>
                    </div>
                </div>
            </section>

             <section id="contact" class="py-20 text-center fade-in-section">
                 <p class="font-mono text-accent mb-4">./contact --send</p>
                 <h2 class="text-4xl font-bold text-white mb-6">Have a project in mind?</h2>
                 <p class="text-lg text-gray-400 max-w-xl mx-auto mb-8">I'm currently open to new opportunities and collaborations. Let's build something amazing together.</p>
                 <a href="mailto:ahmedachbarou842@gmail.com" class="inline-block bg-accent text-black font-bold py-4 px-8 rounded-lg text-lg hover:bg-green-400 transition-colors duration-300">Execute Contact()</a>
            </section>
        </main>
    </div>

    <!-- README Modal -->
    <div id="readme-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden">
        <div id="modal-backdrop" class="absolute inset-0 bg-black/70"></div>
        <div id="modal-content" class="bg-card border border-card rounded-lg shadow-xl w-11/12 md:w-3/4 lg:w-2/3 max-w-4xl max-h-[80vh] flex flex-col transform scale-95 opacity-0">
            <div class="flex justify-between items-center p-4 border-b border-card">
                <h3 class="font-mono text-lg text-white">Generated README.md</h3>
                <button id="close-modal-btn" class="text-gray-400 hover:text-white">&times;</button>
            </div>
            <pre id="modal-body" class="p-6 overflow-y-auto font-mono text-sm whitespace-pre-wrap"></pre>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Matrix Background
            const canvas = document.getElementById('matrix-bg');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            const alphabet = 'アァカサタナハマヤャラワガザダバパイィキシチニヒミリヰギジヂビピウゥクスツヌフムユュルグズブヅプエェケセテネヘメレヱゲゼデベペオォコソトノホモヨョロヲゴゾドボポヴッンABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            const fontSize = 16;
            const columns = canvas.width / fontSize;
            const rainDrops = [];
            for (let x = 0; x < columns; x++) { rainDrops[x] = 1; }
            const drawMatrix = () => {
                ctx.fillStyle = 'rgba(13, 17, 23, 0.05)';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                ctx.fillStyle = '#39D353';
                ctx.font = fontSize + 'px monospace';
                for (let i = 0; i < rainDrops.length; i++) {
                    const text = alphabet.charAt(Math.floor(Math.random() * alphabet.length));
                    ctx.fillText(text, i * fontSize, rainDrops[i] * fontSize);
                    if (rainDrops[i] * fontSize > canvas.height && Math.random() > 0.975) { rainDrops[i] = 0; }
                    rainDrops[i]++;
                }
            };
            setInterval(drawMatrix, 30);
            window.addEventListener('resize', () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; });

            // Typing Effect
            const typingElement = document.getElementById('typing-subtitle');
            const textToType = "/full-stack-developer";
            let i = 0;
            function typeWriter() {
                if (i < textToType.length) {
                    typingElement.innerHTML += textToType.charAt(i);
                    i++;
                    setTimeout(typeWriter, 100);
                } else {
                     typingElement.innerHTML += '<span style="animation: blink-cursor 1s step-end infinite;">_</span>';
                }
            }
            typeWriter();

            // Active Nav Link on Scroll
            const sections = document.querySelectorAll('main section');
            const navLinks = document.querySelectorAll('#desktop-nav a');
            const observer = new IntersectionObserver(entries => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        navLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href').substring(1) === entry.target.id) { link.classList.add('active'); }
                        });
                    }
                });
            }, { threshold: 0.3 });
            sections.forEach(section => observer.observe(section));

            // Fade In on Scroll
            const faders = document.querySelectorAll('.fade-in-section');
            const faderObserver = new IntersectionObserver(entries => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                       entry.target.classList.add('is-visible');
                       faderObserver.unobserve(entry.target);
                    }
                });
            }, { threshold: 0.1 });
            faders.forEach(fader => faderObserver.observe(fader));
            
            // Skills Matrix Tabs
            const skillTabs = document.querySelectorAll('.skill-tab');
            const skillContents = document.querySelectorAll('.skill-content');
            skillTabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    skillTabs.forEach(item => item.classList.remove('active'));
                    tab.classList.add('active');
                    const target = document.getElementById(tab.dataset.tab);
                    skillContents.forEach(content => content.classList.remove('active'));
                    target.classList.add('active');
                });
            });

            // Project Filtering
            const filterButtons = document.querySelectorAll('.filter-btn');
            const projectCards = document.querySelectorAll('.project-card');
            filterButtons.forEach(button => {
                button.addEventListener('click', () => {
                    filterButtons.forEach(btn => btn.classList.remove('bg-accent', 'text-black'));
                    button.classList.add('bg-accent', 'text-black');
                    const filter = button.dataset.filter;
                    projectCards.forEach(card => {
                        const tags = card.dataset.tags;
                        card.style.display = (filter === 'all' || (tags && tags.includes(filter))) ? 'block' : 'none';
                    });
                });
            });

            // Gemini API Call Function
            async function callGemini(prompt, buttonElement, resultContainer) {
                if(buttonElement) buttonElement.disabled = true;
                if(resultContainer) resultContainer.innerHTML = 'Generating response...';

                let chatHistory = [{ role: "user", parts: [{ text: prompt }] }];
                const payload = { contents: chatHistory };
                const apiKey = ""; 
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
                
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    
                    if (!response.ok) throw new Error(`API Error: ${response.statusText}`);
                    
                    const result = await response.json();

                    if (result.candidates && result.candidates[0]?.content?.parts[0]?.text) {
                        return result.candidates[0].content.parts[0].text;
                    } else {
                        return 'Error: Could not retrieve a valid response from the AI.';
                    }
                } catch (error) {
                    console.error("Gemini API call failed:", error);
                    return `An error occurred: ${error.message}.`;
                } finally {
                    if(buttonElement) buttonElement.disabled = false;
                }
            }
            
            // AI README Modal Logic
            const modal = document.getElementById('readme-modal');
            const modalBackdrop = document.getElementById('modal-backdrop');
            const modalBody = document.getElementById('modal-body');
            const closeModalBtn = document.getElementById('close-modal-btn');
            const aiReadmeBtns = document.querySelectorAll('.ai-readme-btn');

            function showModal() {
                modal.classList.remove('hidden');
                setTimeout(() => {
                    modalBackdrop.classList.remove('opacity-0');
                    document.getElementById('modal-content').classList.remove('scale-95', 'opacity-0');
                }, 10);
            }
            function hideModal() {
                modalBackdrop.classList.add('opacity-0');
                document.getElementById('modal-content').classList.add('scale-95', 'opacity-0');
                setTimeout(() => modal.classList.add('hidden'), 300);
            }
            closeModalBtn.addEventListener('click', hideModal);
            modalBackdrop.addEventListener('click', hideModal);

            aiReadmeBtns.forEach(btn => {
                btn.addEventListener('click', async (e) => {
                    const card = e.target.closest('.project-card');
                    const title = card.querySelector('h3').innerText;
                    const description = card.querySelector('p').innerText;
                    const tags = card.querySelector('.font-mono').innerText;
                    
                    showModal();
                    modalBody.textContent = 'Generating README with AI...';

                    const prompt = `You are an expert technical writer. Create a professional GitHub README.md file content for the following project. Use Markdown formatting. Include these sections: a project title, a short description, key features (in a bulleted list based on the description), and tech stack. \n\nProject Title: ${title}\nDescription: ${description}\nTech Stack: ${tags}`;

                    const readmeContent = await callGemini(prompt, btn, modalBody);
                    modalBody.textContent = readmeContent;
                });
            });

            // Interactive Terminal
            const terminalOutput = document.getElementById('terminal-output');
            const terminalInput = document.getElementById('terminal-input');

            function printToTerminal(text, isCommand = false) {
                const line = document.createElement('div');
                line.className = 'terminal-line';
                if (isCommand) {
                    line.innerHTML = `<span class="text-accent">$</span> ${text}`;
                } else {
                    line.innerHTML = text;
                }
                terminalOutput.appendChild(line);
                terminalOutput.scrollTop = terminalOutput.scrollHeight;
            }

            printToTerminal("Welcome to my interactive terminal!");
            printToTerminal("Type 'help' to see available commands.");

            terminalInput.addEventListener('keydown', async function(e) {
                if (e.key === 'Enter') {
                    const command = terminalInput.value.trim().toLowerCase();
                    if (!command) return;
                    printToTerminal(command, true);
                    terminalInput.value = '';
                    await executeCommand(command);
                }
            });
            
            async function executeCommand(command) {
                const commandParts = command.split(' ');
                const baseCommand = commandParts[0];

                if (baseCommand === 'ask') {
                    const question = commandParts.slice(1).join(' ');
                    if (!question) {
                        printToTerminal("Usage: ask <your question>");
                        return;
                    }
                    printToTerminal("<i>AI is thinking...</i>");
                    const prompt = `You are an AI assistant in a developer's portfolio. Answer the following question concisely and helpfully.\n\nQuestion: "${question}"`;
                    const response = await callGemini(prompt);
                    printToTerminal(response);
                    return;
                }
                
                const commandMap = {
                    'help': () => printToTerminal(`Available commands:\n  <span class="text-white">about</span>      - Shows my professional summary.\n  <span class="text-white">services</span>   - Displays the services I offer.\n  <span class="text-white">skills</span>     - Scrolls to my skills section.\n  <span class="text-white">projects</span>   - Scrolls to my featured projects.\n  <span class="text-white">contact</span>    - Shows my email address.\n  <span class="text-white">socials</span>    - Lists my social media links.\n  <span class="text-white">ask</span>        - Ask the AI a question (e.g., ask what is Go).\n  <span class="text-white">clear</span>      - Clears the terminal screen.`),
                    'about': () => printToTerminal("I am a full-stack developer specializing in Go and React."),
                    'services': () => document.getElementById('services').scrollIntoView(),
                    'skills': () => document.getElementById('skills').scrollIntoView(),
                    'projects': () => document.getElementById('projects').scrollIntoView(),
                    'contact': () => printToTerminal(`You can reach me at: <a href="mailto:ahmedachbarou842@gmail.com" class="text-accent underline">ahmedachbarou842@gmail.com</a>`),
                    'socials': () => printToTerminal(`Connect with me:\n  <a href="https://github.com/aachbarou" target="_blank" class="text-accent underline">GitHub</a>\n  <a href="https://linkedin.com/in/ahmed-achbarou" target="_blank" class="text-accent underline">LinkedIn</a>`),
                    'clear': () => terminalOutput.innerHTML = ''
                };
                if (commandMap[baseCommand]) { commandMap[baseCommand](); }
                else { printToTerminal(`Command not found: <span class="text-red-500">${command}</span>. Type 'help' for a list of commands.`); }
            }
        });
    </script>
</body>
</html>
