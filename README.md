<!DOCTYPE html>
<html lang="en">
<head>
    <base target="_self">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QuantumMind | Mathematics & Physics Education Platform</title>
    <meta name="description" content="A modern educational platform for Mathematics and Physics enthusiasts. Explore quantum mechanics, calculus, astrophysics, and number theory with interactive tools and resources.">
    <meta name="keywords" content="mathematics, physics, quantum mechanics, calculus, astrophysics, number theory, education, learning, scientific">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        charcoal: "#121212",
                        "electric-blue": "#0066ff",
                        "neon-teal": "#00ffcc",
                        "grid-line": "rgba(255, 255, 255, 0.05)",
                        "accent-purple": "#9d4edd",
                        "accent-orange": "#ff6b35"
                    },
                    fontFamily: {
                        inter: ["Inter", "sans-serif"],
                        roboto: ["Roboto", "sans-serif"]
                    },
                    backgroundImage: {
                        'grid-pattern': 'linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px)',
                        'pi-watermark': 'url("data:image/svg+xml,%3Csvg width=\'100\' height=\'100\' xmlns=\'http://www.w3.org/2000/svg\'%3E%3Ctext x=\'50%25\' y=\'50%25\' font-family=\'Arial\' font-size=\'14\' fill=\'rgba(255,255,255,0.02)\' text-anchor=\'middle\' dy=\'.3em\'%3Eπ%3C/text%3E%3C/svg%3E")',
                        'phi-watermark': 'url("data:image/svg+xml,%3Csvg width=\'100\' height=\'100\' xmlns=\'http://www.w3.org/2000/svg\'%3E%3Ctext x=\'50%25\' y=\'50%25\' font-family=\'Arial\' font-size=\'14\' fill=\'rgba(255,255,255,0.02)\' text-anchor=\'middle\' dy=\'.3em\'%3EΦ%3C/text%3E%3C/svg%3E")'
                    },
                    animation: {
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'float': 'float 6s ease-in-out infinite',
                        'fractal-spin': 'fractalSpin 20s linear infinite'
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-10px)' }
                        },
                        fractalSpin: {
                            '0%': { transform: 'rotate(0deg) scale(1)' },
                            '50%': { transform: 'rotate(180deg) scale(1.1)' },
                            '100%': { transform: 'rotate(360deg) scale(1)' }
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        
        .focus-mode {
            filter: brightness(0.8) contrast(1.2);
        }
        
        .particle {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, rgba(0, 102, 255, 0.3) 0%, rgba(0, 255, 204, 0.1) 70%, transparent 100%);
            pointer-events: none;
        }
        
        .fractal-bg {
            background: 
                radial-gradient(circle at 20% 30%, rgba(0, 102, 255, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(0, 255, 204, 0.05) 0%, transparent 50%),
                linear-gradient(135deg, rgba(18, 18, 18, 0.95) 0%, rgba(30, 30, 30, 0.95) 100%);
        }
        
        .theory-card {
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .theory-card:hover {
            transform: translateY(-5px);
            border-color: rgba(0, 102, 255, 0.5);
            box-shadow: 0 10px 25px rgba(0, 102, 255, 0.2);
        }
        
        .equation-input {
            font-family: 'Roboto', monospace;
        }
        
        .grid-overlay {
            background-size: 50px 50px;
            background-image: 
                linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
        }
    </style>
</head>
<body class="bg-charcoal text-white min-h-screen">
    <!-- Focus Mode Toggle -->
    <div class="fixed top-4 right-4 z-50">
        <button id="focus-toggle" class="bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors flex items-center gap-2">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
            </svg>
            Focus Mode
        </button>
    </div>

    <!-- Header & Navigation -->
    <header class="sticky top-0 z-40 bg-charcoal/90 backdrop-blur-md border-b border-gray-800">
        <nav class="container mx-auto px-4 py-4">
            <div class="flex justify-between items-center">
                <div class="flex items-center gap-2">
                    <div class="w-8 h-8 rounded-full bg-gradient-to-r from-electric-blue to-neon-teal"></div>
                    <h1 class="text-xl font-bold bg-gradient-to-r from-electric-blue to-neon-teal bg-clip-text text-transparent">QuantumMind</h1>
                </div>
                
                <ul id="nav-list" class="hidden md:flex items-center gap-8"></ul>
                
                <div class="flex items-center gap-4">
                    <button id="mobile-menu-toggle" class="md:hidden text-gray-300 hover:text-white">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                        </svg>
                    </button>
                    <button class="bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors hidden md:block">
                        Sign In
                    </button>
                </div>
            </div>
            
            <!-- Mobile Menu -->
            <div id="mobile-menu" class="md:hidden mt-4 hidden">
                <ul id="mobile-nav-list" class="space-y-2"></ul>
                <div class="mt-4 pt-4 border-t border-gray-800">
                    <button class="w-full bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Sign In
                    </button>
                </div>
            </div>
        </nav>
    </header>

    <main class="relative">
        <!-- Background Grid Overlay -->
        <div class="fixed inset-0 grid-overlay pointer-events-none z-0"></div>
        
        <!-- Hero Section -->
        <section id="hero" class="relative min-h-[90vh] flex items-center justify-center overflow-hidden fractal-bg">
            <div class="absolute inset-0 bg-pi-watermark opacity-10"></div>
            
            <!-- Animated Fractal -->
            <div class="absolute w-64 h-64 md:w-96 md:h-96 opacity-20 animate-fractal-spin">
                <div class="w-full h-full border border-electric-blue/30 rounded-full"></div>
                <div class="absolute top-1/2 left-1/2 w-3/4 h-3/4 border border-neon-teal/30 rounded-full -translate-x-1/2 -translate-y-1/2"></div>
                <div class="absolute top-1/2 left-1/2 w-1/2 h-1/2 border border-accent-purple/30 rounded-full -translate-x-1/2 -translate-y-1/2"></div>
            </div>
            
            <div class="container mx-auto px-4 relative z-10 text-center">
                <h2 class="text-4xl md:text-6xl font-bold mb-6">
                    <span class="bg-gradient-to-r from-electric-blue via-neon-teal to-accent-purple bg-clip-text text-transparent">
                        Explore the Laws<br>of the Universe
                    </span>
                </h2>
                <p class="text-xl text-gray-300 mb-8 max-w-2xl mx-auto">
                    A modern platform for Mathematics and Physics enthusiasts. Dive into interactive theory, solve complex problems, and join a community of curious minds.
                </p>
                <div class="flex flex-col sm:flex-row gap-4 justify-center">
                    <button class="bg-electric-blue hover:bg-blue-600 text-white px-8 py-3 rounded-lg text-lg font-semibold transition-colors transform hover:scale-105">
                        Start Learning
                    </button>
                    <button class="bg-transparent border border-electric-blue text-electric-blue hover:bg-electric-blue/10 px-8 py-3 rounded-lg text-lg font-semibold transition-colors">
                        Watch Introduction
                    </button>
                </div>
                
                <!-- Equation Preview -->
                <div class="mt-12 bg-gray-900/50 backdrop-blur-sm rounded-xl p-6 max-w-2xl mx-auto border border-gray-800">
                    <p class="text-gray-400 mb-2">Try our LaTeX equation renderer:</p>
                    <div class="text-center">
                        <div class="equation-display text-2xl p-4 bg-gray-800/50 rounded-lg mb-4">
                            \[ \nabla \cdot \mathbf{E} = \frac{\rho}{\varepsilon_0} \]
                        </div>
                        <p class="text-sm text-gray-500">Maxwell's First Equation - Gauss's Law for Electricity</p>
                    </div>
                </div>
            </div>
            
            <!-- Particle Container -->
            <div id="particle-container" class="absolute inset-0 pointer-events-none"></div>
        </section>

        <!-- Interactive Theory Hub -->
        <section id="theory-hub" class="py-16 relative">
            <div class="absolute inset-0 bg-phi-watermark opacity-5"></div>
            <div class="container mx-auto px-4 relative z-10">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold mb-4">Interactive Theory Hub</h2>
                    <p class="text-gray-400 max-w-2xl mx-auto">Explore fundamental concepts across major mathematical and physical disciplines with interactive content.</p>
                </div>
                
                <div id="theory-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6"></div>
            </div>
        </section>

        <!-- Problem Solver Dashboard -->
        <section id="problem-solver" class="py-16 bg-gray-900/30">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold mb-4">Problem Solver Dashboard</h2>
                    <p class="text-gray-400 max-w-2xl mx-auto">Input equations in LaTeX format and get step-by-step solutions with our integrated math engine.</p>
                </div>
                
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="bg-gray-900/50 backdrop-blur-sm rounded-xl p-6 border border-gray-800">
                        <h3 class="text-xl font-bold mb-4 text-electric-blue">Equation Input</h3>
                        <div class="space-y-4">
                            <div>
                                <label class="block text-gray-400 mb-2">Enter LaTeX Equation</label>
                                <textarea id="equation-input" class="w-full bg-gray-800 border border-gray-700 rounded-lg p-4 equation-input text-lg" rows="3" placeholder="E = mc^2"></textarea>
                            </div>
                            <div>
                                <label class="block text-gray-400 mb-2">Equation Preview</label>
                                <div id="equation-preview" class="w-full bg-gray-800 border border-gray-700 rounded-lg p-4 min-h-[100px] flex items-center justify-center">
                                    <p class="text-gray-500">Your equation will appear here</p>
                                </div>
                            </div>
                            <button id="solve-equation" class="w-full bg-neon-teal hover:bg-teal-500 text-gray-900 font-bold py-3 rounded-lg transition-colors">
                                Solve Equation
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-gray-900/50 backdrop-blur-sm rounded-xl p-6 border border-gray-800">
                        <h3 class="text-xl font-bold mb-4 text-neon-teal">Recent Solutions</h3>
                        <div id="recent-solutions" class="space-y-4"></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Resource Library -->
        <section id="resource-library" class="py-16">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold mb-4">Resource Library</h2>
                    <p class="text-gray-400 max-w-2xl mx-auto">Access curated PDFs, cheat sheets, and simulation links for deeper learning.</p>
                </div>
                
                <div class="mb-8">
                    <div class="flex flex-wrap gap-2 mb-6">
                        <button class="resource-filter active px-4 py-2 rounded-lg bg-electric-blue text-white" data-filter="all">All Resources</button>
                        <button class="resource-filter px-4 py-2 rounded-lg bg-gray-800 hover:bg-gray-700" data-filter="pdf">PDFs</button>
                        <button class="resource-filter px-4 py-2 rounded-lg bg-gray-800 hover:bg-gray-700" data-filter="cheatsheet">Cheat Sheets</button>
                        <button class="resource-filter px-4 py-2 rounded-lg bg-gray-800 hover:bg-gray-700" data-filter="simulation">Simulations</button>
                    </div>
                </div>
                
                <div id="resource-list" class="space-y-4"></div>
            </div>
        </section>

        <!-- Community Forum -->
        <section id="community-forum" class="py-16 bg-gray-900/30">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl md:text-4xl font-bold mb-4">Community Forum</h2>
                    <p class="text-gray-400 max-w-2xl mx-auto">Join discussions, share insights, and tackle the "Problem of the Day" with fellow enthusiasts.</p>
                </div>
                
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="lg:col-span-2">
                        <div class="bg-gradient-to-r from-gray-900 to-charcoal rounded-xl p-6 border border-gray-800 mb-8">
                            <div class="flex items-center justify-between mb-4">
                                <h3 class="text-xl font-bold text-electric-blue">Problem of the Day</h3>
                                <span class="bg-neon-teal text-gray-900 px-3 py-1 rounded-full text-sm font-bold">Active</span>
                            </div>
                            <div class="mb-4">
                                <div class="text-2xl mb-4 text-center">
                                    \[ \int_0^\infty \frac{\sin(x)}{x} \, dx \]
                                </div>
                                <p class="text-gray-300">Evaluate the Dirichlet integral. This classic problem appears in signal processing and Fourier analysis.</p>
                            </div>
                            <div class="flex justify-between items-center">
                                <div class="text-sm text-gray-400">
                                    <span class="text-neon-teal">42</span> solutions submitted
                                </div>
                                <button class="bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-medium">
                                    Submit Solution
                                </button>
                            </div>
                        </div>
                        
                        <div id="forum-discussions" class="space-y-4"></div>
                    </div>
                    
                    <div>
                        <div class="bg-gray-900/50 backdrop-blur-sm rounded-xl p-6 border border-gray-800 sticky top-24">
                            <h3 class="text-xl font-bold mb-4 text-neon-teal">Top Contributors</h3>
                            <div id="top-contributors" class="space-y-4"></div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-900 border-t border-gray-800 py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
                <div>
                    <div class="flex items-center gap-2 mb-4">
                        <div class="w-8 h-8 rounded-full bg-gradient-to-r from-electric-blue to-neon-teal"></div>
                        <h3 class="text-xl font-bold">QuantumMind</h3>
                    </div>
                    <p class="text-gray-400 text-sm">A modern educational platform for Mathematics and Physics enthusiasts.</p>
                </div>
                
                <div>
                    <h4 class="font-bold mb-4 text-electric-blue">Quick Links</h4>
                    <ul id="footer-quick-links" class="space-y-2"></ul>
                </div>
                
                <div>
                    <h4 class="font-bold mb-4 text-neon-teal">Subjects</h4>
                    <ul id="footer-subjects" class="space-y-2"></ul>
                </div>
                
                <div>
                    <h4 class="font-bold mb-4 text-accent-purple">Connect</h4>
                    <div class="flex gap-4 mb-4">
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 hover:bg-electric-blue flex items-center justify-center transition-colors">
                            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/>
                            </svg>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 hover:bg-blue-600 flex items-center justify-center transition-colors">
                            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                            </svg>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 hover:bg-red-600 flex items-center justify-center transition-colors">
                            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
                            </svg>
                        </a>
                    </div>
                    <p class="text-gray-400 text-sm">Subscribe to our newsletter for updates</p>
                    <div class="mt-4 flex">
                        <input type="email" placeholder="Your email" class="flex-grow bg-gray-800 border border-gray-700 rounded-l-lg px-4 py-2 text-sm">
                        <button class="bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-r-lg text-sm font-medium">
                            Subscribe
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="pt-8 border-t border-gray-800 text-center text-gray-500 text-sm">
                <p>&copy; 2023 QuantumMind. All rights reserved. | Designed for Mathematics & Physics enthusiasts</p>
                <p class="mt-2">This site uses MathJax for LaTeX rendering and follows WCAG 2.1 accessibility guidelines.</p>
            </div>
        </div>
    </footer>

    <script>
        // ==================== DATA LAYER ====================
        const navigationItems = [
            { "label": "Home", "href": "#hero" },
            { "label": "Theory Hub", "href": "#theory-hub" },
            { "label": "Problem Solver", "href": "#problem-solver" },
            { "label": "Resources", "href": "#resource-library" },
            { "label": "Community", "href": "#community-forum" }
        ];

        const theoryCategories = [
            { 
                "title": "Quantum Mechanics", 
                "description": "Wave functions, superposition, and quantum entanglement",
                "icon": "⚛️",
                "color": "electric-blue",
                "topics": 24,
                "image": "https://picsum.photos/400/300?random=101"
            },
            { 
                "title": "Calculus", 
                "description": "Limits, derivatives, integrals, and series",
                "icon": "∫",
                "color": "neon-teal",
                "topics": 18,
                "image": "https://picsum.photos/400/300?random=102"
            },
            { 
                "title": "Astrophysics", 
                "description": "Cosmology, stellar evolution, and relativity",
                "icon": "🌌",
                "color": "accent-purple",
                "topics": 16,
                "image": "https://picsum.photos/400/300?random=103"
            },
            { 
                "title": "Number Theory", 
                "description": "Primes, modular arithmetic, and Diophantine equations",
                "icon": "#",
                "color": "accent-orange",
                "topics": 22,
                "image": "https://picsum.photos/400/300?random=104"
            }
        ];

        const recentSolutions = [
            { 
                "equation": "\\frac{d^2y}{dx^2} + 4y = \\sin(2x)", 
                "subject": "Differential Equations",
                "solved": "2 hours ago",
                "difficulty": "Intermediate"
            },
            { 
                "equation": "\\nabla \\times \\mathbf{B} = \\mu_0\\mathbf{J} + \\mu_0\\varepsilon_0\\frac{\\partial \\mathbf{E}}{\\partial t}", 
                "subject": "Electromagnetism",
                "solved": "Yesterday",
                "difficulty": "Advanced"
            },
            { 
                "equation": "\\sum_{n=1}^\\infty \\frac{1}{n^2} = \\frac{\\pi^2}{6}", 
                "subject": "Infinite Series",
                "solved": "3 days ago",
                "difficulty": "Intermediate"
            }
        ];

        const resources = [
            { 
                "title": "Quantum Mechanics Primer", 
                "type": "pdf",
                "size": "4.2 MB",
                "description": "Introduction to wave functions and Schrödinger equation",
                "downloads": 1243
            },
            { 
                "title": "Calculus Cheat Sheet", 
                "type": "cheatsheet",
                "size": "1.1 MB",
                "description": "All essential derivatives and integrals",
                "downloads": 3567
            },
            { 
                "title": "Orbital Mechanics Simulation", 
                "type": "simulation",
                "size": "Interactive",
                "description": "Visualize planetary orbits and gravitational effects",
                "downloads": 892
            },
            { 
                "title": "Statistical Mechanics PDF", 
                "type": "pdf",
                "size": "8.7 MB",
                "description": "Thermodynamics and probability distributions",
                "downloads": 567
            },
            { 
                "title": "Linear Algebra Reference", 
                "type": "cheatsheet",
                "size": "2.3 MB",
                "description": "Matrix operations and vector spaces",
                "downloads": 2345
            },
            { 
                "title": "Quantum Field Theory Notes", 
                "type": "pdf",
                "size": "12.4 MB",
                "description": "Advanced topics in particle physics",
                "downloads": 321
            }
        ];

        const forumDiscussions = [
            { 
                "title": "Interpretation of Quantum Mechanics", 
                "author": "Dr. Elena Rodriguez",
                "replies": 42,
                "lastActivity": "2 hours ago",
                "category": "Quantum Physics"
            },
            { 
                "title": "Help with Fourier Transform Problem", 
                "author": "Alex Chen",
                "replies": 18,
                "lastActivity": "5 hours ago",
                "category": "Mathematics"
            },
            { 
                "title": "Dark Matter Evidence Discussion", 
                "author": "Prof. James Wilson",
                "replies": 67,
                "lastActivity": "Yesterday",
                "category": "Astrophysics"
            },
            { 
                "title": "Best Resources for Tensor Calculus", 
                "author": "Maria Santos",
                "replies": 23,
                "lastActivity": "2 days ago",
                "category": "Mathematics"
            }
        ];

        const topContributors = [
            { 
                "name": "Dr. Elena Rodriguez", 
                "role": "Quantum Physicist",
                "solutions": 142,
                "avatar": "https://picsum.photos/50?random=201"
            },
            { 
                "name": "Alex Chen", 
                "role": "Mathematics Graduate",
                "solutions": 89,
                "avatar": "https://picsum.photos/50?random=202"
            },
            { 
                "name": "Prof. James Wilson", 
                "role": "Astrophysicist",
                "solutions": 76,
                "avatar": "https://picsum.photos/50?random=203"
            },
            { 
                "name": "Maria Santos", 
                "role": "Theoretical Physics Student",
                "solutions": 65,
                "avatar": "https://picsum.photos/50?random=204"
            }
        ];

        const footerQuickLinks = [
            { "label": "About Us", "href": "#" },
            { "label": "Contact", "href": "#" },
            { "label": "Privacy Policy", "href": "#" },
            { "label": "Terms of Service", "href": "#" },
            { "label": "FAQ", "href": "#" }
        ];

        const footerSubjects = [
            { "label": "Algebra", "href": "#" },
            { "label": "Geometry", "href": "#" },
            { "label": "Trigonometry", "href": "#" },
            { "label": "Statistics", "href": "#" },
            { "label": "Mechanics", "href": "#" }
        ];

        // ==================== REUSABLE RENDER FUNCTIONS ====================
        function renderNavItems(items) {
            return items.map(item => 
                `<li><a href="${item.href}" class="text-gray-300 hover:text-electric-blue transition-colors font-medium">${item.label}</a></li>`
            ).join("");
        }

        function renderTheoryCards(items) {
            return items.map(item => `
                <div class="theory-card bg-gray-900/50 backdrop-blur-sm rounded-xl p-6 hover:shadow-2xl">
                    <div class="flex items-start justify-between mb-4">
                        <div class="text-4xl">${item.icon}</div>
                        <span class="px-3 py-1 bg-${item.color}/20 text-${item.color} rounded-full text-sm font-medium">${item.topics} topics</span>
                    </div>
                    <h3 class="text-xl font-bold mb-2">${item.title}</h3>
                    <p class="text-gray-400 mb-4">${item.description}</p>
                    <div class="mt-6 pt-4 border-t border-gray-800">
                        <img src="${item.image}" alt="${item.title} illustration" class="w-full h-40 object-cover rounded-lg" loading="lazy">
                    </div>
                    <button class="mt-4 w-full bg-gray-800 hover:bg-${item.color} text-white py-2 rounded-lg transition-colors">
                        Explore ${item.title}
                    </button>
                </div>
            `).join("");
        }

        function renderRecentSolutions(items) {
            return items.map(item => `
                <div class="bg-gray-800/50 rounded-lg p-4 border border-gray-700">
                    <div class="text-lg mb-2">${item.equation}</div>
                    <div class="flex justify-between items-center text-sm text-gray-400">
                        <span>${item.subject}</span>
                        <span class="px-2 py-1 bg-gray-700 rounded">${item.difficulty}</span>
                    </div>
                    <div class="text-xs text-gray-500 mt-2">Solved ${item.solved}</div>
                </div>
            `).join("");
        }

        function renderResourceList(items) {
            return items.map(item => `
                <div class="resource-item bg-gray-900/50 backdrop-blur-sm rounded-xl p-4 border border-gray-800" data-type="${item.type}">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 rounded-lg bg-gray-800 flex items-center justify-center">
                                ${item.type === 'pdf' ? '📄' : item.type === 'cheatsheet' ? '📋' : '🖥️'}
                            </div>
                            <div>
                                <h4 class="font-bold">${item.title}</h4>
                                <p class="text-sm text-gray-400">${item.description}</p>
                                <div class="flex items-center gap-4 mt-1 text-xs text-gray-500">
                                    <span>${item.size}</span>
                                    <span>${item.downloads.toLocaleString()} downloads</span>
                                </div>
                            </div>
                        </div>
                        <button class="bg-electric-blue hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                            ${item.type === 'simulation' ? 'Launch' : 'Download'}
                        </button>
                    </div>
                </div>
            `).join("");
        }

        function renderForumDiscussions(items) {
            return items.map(item => `
                <div class="bg-gray-900/50 backdrop-blur-sm rounded-xl p-4 border border-gray-800">
                    <div class="flex justify-between items-start">
                        <div>
                            <h4 class="font-bold mb-1">${item.title}</h4>
                            <div class="flex items-center gap-4 text-sm text-gray-400">
                                <span>by ${item.author}</span>
                                <span class="px-2 py-1 bg-gray-800 rounded">${item.category}</span>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="text-lg font-bold text-neon-teal">${item.replies}</div>
                            <div class="text-xs text-gray-500">replies</div>
                        </div>
                    </div>
                    <div class="text-xs text-gray-500 mt-2">Last activity: ${item.lastActivity}</div>
                </div>
            `).join("");
        }

        function renderTopContributors(items) {
            return items.map(item => `
                <div class="flex items-center gap-3">
                    <img src="${item.avatar}" alt="${item.name}" class="w-10 h-10 rounded-full" loading="lazy">
                    <div class="flex-grow">
                        <div class="font-medium">${item.name}</div>
                        <div class="text-sm text-gray-400">${item.role}</div>
                    </div>
                    <div class="text-right">
                        <div class="text-electric-blue font-bold">${item.solutions}</div>
                        <div class="text-xs text-gray-500">solutions</div>
                    </div>
                </div>
            `).join("");
        }

        function renderFooterLinks(items) {
            return items.map(item => 
                `<li><a href="${item.href}" class="text-gray-400 hover:text-white text-sm transition-colors">${item.label}</a></li>`
            ).join("");
        }

        // ==================== INITIALIZATION ====================
        document.addEventListener('DOMContentLoaded', function() {
            // Render navigation
            document.getElementById('nav-list').innerHTML = renderNavItems(navigationItems);
            document.getElementById('mobile-nav-list').innerHTML = renderNavItems(navigationItems);
            
            // Render theory hub
            document.getElementById('theory-grid').innerHTML = renderTheoryCards(theoryCategories);
            
            // Render recent solutions
            document.getElementById('recent-solutions').innerHTML = renderRecentSolutions(recentSolutions);
            
            // Render resources
            document.getElementById('resource-list').innerHTML = renderResourceList(resources);
            
            // Render forum discussions
            document.getElementById('forum-discussions').innerHTML = renderForumDiscussions(forumDiscussions);
            
            // Render top contributors
            document.getElementById('top-contributors').innerHTML = renderTopContributors(topContributors);
            
            // Render footer links
            document.getElementById('footer-quick-links').innerHTML = renderFooterLinks(footerQuickLinks);
            document.getElementById('footer-subjects').innerHTML = renderFooterLinks(footerSubjects);
            
            // Initialize MathJax
            if (window.MathJax) {
                MathJax.typesetPromise();
            }
            
            // Create particle background
            createParticles();
            
            // Initialize event listeners
            initializeEventListeners();
        });

        // ==================== PARTICLE ANIMATION ====================
        function createParticles() {
            const container = document.getElementById('particle-container');
            const particleCount = 50;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                const size = Math.random() * 60 + 20;
                const x = Math.random() * 100;
                const y = Math.random() * 100;
                const duration = Math.random() * 20 + 10;
                
                particle.style.width = `${size}px`;
                particle.style.height = `${size}px`;
                particle.style.left = `${x}%`;
                particle.style.top = `${y}%`;
                particle.style.animation = `float ${duration}s ease-in-out infinite`;
                particle.style.animationDelay = `${Math.random() * 5}s`;
                particle.style.opacity = Math.random() * 0.3 + 0.1;
                
                container.appendChild(particle);
            }
        }

        // ==================== EVENT HANDLERS ====================
        function initializeEventListeners() {
            // Mobile menu toggle
            document.getElementById('mobile-menu-toggle').addEventListener('click', function() {
                const menu = document.getElementById('mobile-menu');
                menu.classList.toggle('hidden');
            });
            
            // Focus mode toggle
            document.getElementById('focus-toggle').addEventListener('click', function() {
                document.body.classList.toggle('focus-mode');
                const button = document.getElementById('focus-toggle');
                if (document.body.classList.contains('focus-mode')) {
                    button.innerHTML = '<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path></svg> Normal Mode';
                    button.classList.remove('bg-electric-blue');
                    button.classList.add('bg-neon-teal', 'text-gray-900');
                } else {
                    button.innerHTML = '<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path></svg> Focus Mode';
                    button.classList.remove('bg-neon-teal', 'text-gray-900');
                    button.classList.add('bg-electric-blue');
                }
            });
            
            // Equation input and preview
            const equationInput = document.getElementById('equation-input');
            const equationPreview = document.getElementById('equation-preview');
            
            equationInput.addEventListener('input', function() {
                const equation = equationInput.value.trim();
                if (equation) {
                    equationPreview.innerHTML = `\\[ ${equation} \\]`;
                    if (window.MathJax) {
                        MathJax.typesetPromise([equationPreview]).catch(err => {
                            equationPreview.innerHTML = '<p class="text-red-400">Invalid LaTeX syntax</p>';
                        });
                    }
                } else {
                    equationPreview.innerHTML = '<p class="text-gray-500">Your equation will appear here</p>';
                }
            });
            
            // Solve equation button
            document.getElementById('solve-equation').addEventListener('click', function() {
                const equation = equationInput.value.trim();
                if (!equation) {
                    alert('Please enter an equation to solve');
                    return;
                }
                
                // Simulate solving process
                const button = document.getElementById('solve-equation');
                const originalText = button.textContent;
                button.textContent = 'Solving...';
                button.disabled = true;
                
                setTimeout(() => {
                    button.textContent = 'Solved!';
                    button.classList.remove('bg-neon-teal', 'hover:bg-teal-500');
                    button.classList.add('bg-green-500');
                    
                    // Add to recent solutions
                    const newSolution = {
                        equation: equation,
                        subject: "User Input",
                        solved: "Just now",
                        difficulty: "User"
                    };
                    
                    // Update recent solutions
                    recentSolutions.unshift(newSolution);
                    if (recentSolutions.length > 3) recentSolutions.pop();
                    document.getElementById('recent-solutions').innerHTML = renderRecentSolutions(recentSolutions);
                    
                    // Reset button after delay
                    setTimeout(() => {
                        button.textContent = originalText;
                        button.disabled = false;
                        button.classList.remove('bg-green-500');
                        button.classList.add('bg-neon-teal', 'hover:bg-teal-500');
                    }, 2000);
                }, 1500);
            });
            
            // Resource filtering
            const filterButtons = document.querySelectorAll('.resource-filter');
            const resourceItems = document.querySelectorAll('.resource-item');
            
            filterButtons.forEach(button => {
                button.addEventListener('click', function() {
                    // Update active button
                    filterButtons.forEach(btn => {
                        btn.classList.remove('active', 'bg-electric-blue', 'text-white');
                        btn.classList.add('bg-gray-800', 'hover:bg-gray-700');
                    });
                    this.classList.add('active', 'bg-electric-blue', 'text-white');
                    this.classList.remove('bg-gray-800', 'hover:bg-gray-700');
                    
                    // Filter resources
                    const filter = this.dataset.filter;
                    resourceItems.forEach(item => {
                        if (filter === 'all' || item.dataset.type === filter) {
                            item.style.display = 'block';
                        } else {
                            item.style.display = 'none';
                        }
                    });
                });
            });
            
            // Smooth scrolling for navigation links (delegated event handling)
            document.addEventListener('click', function(event) {
                const link = event.target.closest('a[href^="#"]');
                if (!link) return;
                
                const href = link.getAttribute('href');
                if (href === '#') return;
                
                event.preventDefault();
                const target = document.querySelector(href);
                if (target) {
                    // Close mobile menu if open
                    const mobileMenu = document.getElementById('mobile-menu');
                    if (!mobileMenu.classList.contains('hidden')) {
                        mobileMenu.classList.add('hidden');
                    }
                    
                    // Smooth scroll to target
                    window.scrollTo({
                        top: target.offsetTop - 80,
                        behavior: 'smooth'
                    });
                }
            });
            
            // Initialize with some sample equations
            const sampleEquations = [
                "E = mc^2",
                "\\int_{-\\infty}^{\\infty} e^{-x^2} dx = \\sqrt{\\pi}",
                "\\nabla \\cdot \\mathbf{E} = \\frac{\\rho}{\\varepsilon_0}"
            ];
            
            // Cycle through sample equations
            let eqIndex = 0;
            function cycleSampleEquations() {
                equationInput.value = sampleEquations[eqIndex];
                equationInput.dispatchEvent(new Event('input'));
                eqIndex = (eqIndex + 1) % sampleEquations.length;
            }
            
            // Set initial sample equation
            cycleSampleEquations();
            
            // Change sample equation every 10 seconds
            setInterval(cycleSampleEquations, 10000);
        }
    </script>
</body>
</html>
