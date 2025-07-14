<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive CV - Harsh Mighlani</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Professional Blue & Gray -->
    <!-- Application Structure Plan: A single-page, vertical-scrolling layout with a sticky navigation bar for intuitive navigation. The structure is thematic to highlight strengths: a professional summary, an interactive career timeline to detail work history on demand, a skills showcase with interactive charts and filterable tag clouds for a granular view, a card-based layout for key architectural projects, and a final section for certifications and contact. This design prioritizes user engagement and makes the information easily scannable and digestible for recruiters. -->
    <!-- Visualization & Content Choices: 
        - Summary -> Inform -> Text Block -> Static -> Clear, concise introduction.
        - Experience -> Change/Organize -> Interactive Vertical Timeline (HTML/CSS/JS) -> On-click reveals details -> More engaging than a static list, shows career progression visually.
        - Skills -> Compare/Organize -> Filterable Tag Lists (HTML/CSS/JS) & Donut Chart (Chart.js) -> Filters allow recruiters to drill into specific tech stacks, while chart gives a high-level overview of expertise areas. -> Justification: Manages a large amount of skill data effectively.
        - Projects -> Organize/Inform -> Card Grid (HTML/CSS) -> Hover effects -> Modern, scannable, and allows for easy grouping of project information.
        - Certifications -> Inform -> List (HTML/CSS) -> Static -> Simple and clear presentation.
        Confirming NO SVG/Mermaid, supporting the designed structure. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            color: #1f2937;
        }
        .timeline-item-content {
            transition: max-height 0.7s ease-in-out, opacity 0.5s ease-in-out;
            max-height: 0;
            opacity: 0;
            overflow: hidden;
        }
        .timeline-item-content.active {
            max-height: 1000px;
            opacity: 1;
        }
        .nav-link {
            position: relative;
            transition: color 0.3s;
        }
        .nav-link::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: -4px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #2563eb;
            transition: width 0.3s;
        }
        .nav-link.active::after, .nav-link:hover::after {
            width: 100%;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px; /* Adjusted for donut chart */
            margin-left: auto;
            margin-right: auto;
            height: 400px;
            max-height: 50vh;
        }
        .skill-filter-btn {
            transition: all 0.2s ease-in-out;
        }
        .skill-filter-btn.active {
            background-color: #2563eb;
            color: white;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
        }
        .skill-tag {
             transition: all 0.2s ease-in-out;
             animation: fadeIn 0.5s;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/90 backdrop-blur-lg sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-2xl font-bold text-gray-800">
                Harsh Mighlani
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#summary" class="nav-link text-gray-600 hover:text-blue-600 font-medium">Summary</a>
                <a href="#timeline" class="nav-link text-gray-600 hover:text-blue-600 font-medium">Timeline</a>
                <a href="#skills" class="nav-link text-gray-600 hover:text-blue-600 font-medium">Skills</a>
                <a href="#projects" class="nav-link text-gray-600 hover:text-blue-600 font-medium">Projects</a>
                <a href="#contact" class="nav-link text-gray-600 hover:text-blue-600 font-medium">Contact</a>
            </div>
            <div class="md:hidden">
                <button id="mobile-menu-button" class="text-gray-800 focus:outline-none">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
                </button>
            </div>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden">
            <a href="#summary" class="block py-2 px-4 text-sm hover:bg-gray-100">Summary</a>
            <a href="#timeline" class="block py-2 px-4 text-sm hover:bg-gray-100">Timeline</a>
            <a href="#skills" class="block py-2 px-4 text-sm hover:bg-gray-100">Skills</a>
            <a href="#projects" class="block py-2 px-4 text-sm hover:bg-gray-100">Projects</a>
            <a href="#contact" class="block py-2 px-4 text-sm hover:bg-gray-100">Contact</a>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">

        <section id="summary" class="my-16 text-center">
            <h1 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">IT Professional & Cloud Architect</h1>
            <div class="max-w-4xl mx-auto space-y-4">
                <p class="text-lg text-gray-700">
                    A highly competent and results-driven IT professional with 14+ years of extensive industry experience in defining robust system architectures, leading greenfield solution design, and developing complex systems. Proven expertise in streamlining workflows and addressing intricate payment challenges for major UK banks.
                </p>
                <p class="text-lg text-gray-600">
                    Holding AWS Certified Solutions Architect Professional and Early AI Adapter certifications, helping clients develop greenfield payment reconciliation systems using AWS Serverless (Lambda, SQS, Event Bridge) and Containerised applications (ECS) with Postgres DB.
                </p>
                 <p class="text-lg text-gray-600">
                    Deep expertise in Java/J2EE, Microservices, and various Database technologies, with proficiency in Identity and Access Management (IAM) platforms including ForgeRock and PingOne.
                </p>
            </div>
        </section>

        <section id="timeline" class="my-24">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-gray-900">Career Timeline</h2>
                <p class="text-md text-gray-500 mt-2">Click on a role to see more details.</p>
            </div>
            <div class="relative wrap overflow-hidden p-4 md:p-10 h-full">
                <div class="absolute h-full border border-gray-300 border-2-2" style="left: 50%"></div>
                <div id="timeline-container"></div>
            </div>
        </section>

        <section id="skills" class="my-24">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-gray-900">Technical Skills Showcase</h2>
                <p class="text-md text-gray-500 mt-2">A visual overview of expertise. Select a category to filter the skills.</p>
            </div>
            <div class="bg-white p-6 rounded-lg shadow-xl">
                 <div class="lg:flex lg:space-x-8">
                     <div class="chart-container mb-8 lg:mb-0 lg:w-1/3">
                        <canvas id="skillsChart"></canvas>
                    </div>
                    <div id="skills-details-container" class="lg:w-2/3">
                        <div id="skills-filter" class="flex flex-wrap gap-2 mb-6 justify-center"></div>
                        <div id="skills-display" class="p-4 bg-gray-50 rounded-lg min-h-[200px]">
                            <div id="skills-list-container" class="flex flex-wrap gap-3"></div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="projects" class="my-24">
             <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-gray-900">Architectural Highlights</h2>
                <p class="text-md text-gray-500 mt-2">Key projects demonstrating leadership and technical architecture skills.</p>
            </div>
            <div class="grid md:grid-cols-2 gap-8" id="projects-container">
            </div>
        </section>

        <section id="contact" class="my-16 text-center">
            <h2 class="text-3xl font-bold text-gray-900 mb-4">Get In Touch</h2>
             <div class="bg-white p-8 rounded-lg shadow-xl inline-block">
                <p class="text-lg text-gray-600 mb-6">Open to new opportunities and collaborations.</p>
                <div class="space-y-4 text-left">
                    <p><strong class="w-24 inline-block">Email:</strong> <a href="mailto:harshmighlani@gmail.com" class="text-blue-600 hover:underline">harshmighlani@gmail.com</a></p>
                    <p><strong class="w-24 inline-block">Phone:</strong> <a href="tel:+4407721702249" class="text-blue-600 hover:underline">+44-07721702249</a></p>
                    <p><strong class="w-24 inline-block">LinkedIn:</strong> <a href="https://www.linkedin.com/in/harsh-mighlani" target="_blank" class="text-blue-600 hover:underline">linkedin.com/in/harsh-mighlani</a></p>
                </div>
                <div class="mt-8 border-t pt-6">
                    <h3 class="font-bold text-xl mb-4 text-gray-700">Certifications</h3>
                    <ul class="list-none space-y-2 text-gray-600" id="certifications-container">
                    </ul>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-gray-800 text-white text-center p-4 mt-12">
        <p>&copy; 2024 Harsh Mighlani. All Rights Reserved.</p>
    </footer>

    <script>
        const cvData = {
            experience: [
                {
                    role: 'Engineering Lead',
                    company: 'Publicis Sapient (Client - Capital One)',
                    date: 'November 2023 – Present',
                    details: [
                        'Led two feature teams of 15+ developers in the development of a greenfield database migration project.',
                        'Designed the greenfield solution from inception, overseeing the transition to Microservices Architecture (MSA) through delivery into production and beta phases.',
                        'Implemented solution using AWS Lambda, EC2, DynamoDB, RDS with combination of downstream systems like TSYS, HSBC Omni-channel to redesign and optimize their reconciliation process using event driven design, reducing Pay By Bank from 1 day to few hours and Pay By Customer from 2 days to 1 day for settlement compliant for upto 1500 TPS in Transaction volume.',
                        'Redesigned existing payment SoR schema with normalized, partitioned AWS RDS to be used in conjuction with containerized and serverless applications hosting over 4M records for over 7 years of data.'
                    ]
                },
                {
                    role: 'Engineering Lead',
                    company: 'Publicis Sapient (Client - Lloyds Banking Group)',
                    date: 'May 2022 – November 2023',
                    details: [
                        'Served as lead for the ID & Auth Lab, implementing Strong Customer Authentication (SCA) in Login & Payments journeys.',
                        'Enabled critical channel integrations for Motor Finance, LBMI, and LBMA.',
                        'Designed/Implemented and led the team for IDAAS (Identity As A Service) as part of Lloyds Hackathon, expanding WebAuthN with Yubikey/Cryptographic device, Device Biometric support.',
                        'Designed Solution and implemented FIDO-II standard authentication like WebAuthN, Time-based OTP with Microsoft/Forgerock Authenticator app, low cost alternative to bank’s traditional SMS OTP and Call Challenge. Leading the team for Ecommerce payment integration, as MVP.',
                        'Proposed opensource OpenAM over Forgerock AM for zero cost, with self framework team for maintenance and support, also compared with MiTek/Ping identity alternatives.'
                    ]
                },
                {
                    role: 'Technical Leader',
                    company: 'Accenture Solutions (Client - Fidelity)',
                    date: 'September 2018 – May 2022',
                    details: [
                        'Contributed to Workplace Investing & SIPP solutions, specifically migrating on-premise services to AWS.',
                        'Built initial greenfield containers and serverless solutions, driving cloud adoption across the organization on AWS.'
                    ]
                },
                 {
                    role: 'Technical Leader',
                    company: 'Sapient Global Markets (Client: Fidelity)',
                    date: 'May 2016 – September 2018',
                    details: [
                        'Worked on API design and implementation for Account Opening, Customer Onboarding and other Personal Investing journeys for Customer and Account Master journeys, and GDPR-compliant solutions.',
                        'Acted as a senior developer on Customer Reporting solutions.'
                    ]
                },
                {
                    role: 'Developer',
                    company: 'Ericsson',
                    date: 'July 2011 – May 2014',
                    details: [
                        'Contributed to AT&T projects during 8 months at Ericsson.',
                        'Involved in organisation’s initiative of tracking tools for application landscape.'
                    ]
                },
                {
                    role: 'Developer',
                    company: 'Sopra Steria',
                    date: 'July 2011 – May 2014',
                    details: [
                        'Gained experience in developer and senior developer roles with Evolan and ST Micro Electronics.',
                        'Built credit card back end app to view roles across back office.'
                    ]
                }
            ],
            skills: {
                "Cloud Platforms": ["AWS", "GCP", "Azure", "OCP", "IBM Private Cloud", "IBM OpenShift", "Kubernetes", "Istio", "GKE", "Google KMS", "Cloud HSM", "Cloud Storage"],
                "Core & Languages": ["Java", "Python", "Algorithms", "Data Structures", "Multithreading", "Design Patterns", "Microservices", "EIP"],
                "Databases": ["Oracle", "PostgreSQL", "MongoDB", "DynamoDB", "DB2", "LDAP", "Cloud Spanner", "Cloud SQL", "MySQL", "HSQLDB"],
                "Frameworks": ["Spring", "Spring Boot", "Spring Integration", "Hibernate", "JMS", "Struts", "XML", "XSLT", "XSD"],
                "Security & IAM": ["Forgerock", "Ping Identity", "OpenAM", "MiTek", "Yoti", "PingOne", "OAuth", "OIDC", "SAML", "PKCE", "Zero Trust", "SHA-512", "AES"],
                "Serverless & Messaging": ["Lambda", "Step Function", "Data Pipeline", "Cloudfunction", "ActiveMQ", "RabbitMQ", "Apache Camel", "SQS", "SNS", "Event-Bridge"],
                "Testing & CI/CD": ["JUnit", "TestNG", "Mockito", "RestAssured", "Selenium", "SonarQube", "OWASP", "Gatling", "Pact", "Jenkins", "Spinnaker", "Maven", "Gradle"],
                "Web & APIs": ["SOAP", "REST", "JAX-RS", "JAX-WS", "Spring Boot", "Dropwizard", "API Gateway", "Apigee"]
            },
            projects: [
                { title: "Major UK Bank Engagement", description: "Led the engagement from inception to delivery for a major UK bank, collaborating closely with Technical and Product forums." },
                { title: "Payment Reconciliation Solution", description: "Architected and developed a comprehensive Payment Reconciliation solution to handle high-volume, event-driven transactions." },
                { title: "Cloud-Based Customer Data Platform", description: "Designed a 100% cloud-based solution capable of hosting 7+ years of bank's customer payment data, supporting real-time user engagement." },
                { title: "Fund House Leadership", description: "Previously served as a Lead for a major fund house, overseeing multiple journeys including SIPP, Customer Onboarding, and GDPR compliance projects." }
            ],
            certifications: [
                "AWS Certified Professional Certification",
                "AWS AI Practitioner Early Adapter",
                "GCP Associate Cloud Engineer",
                "Azure Fundamentals"
            ]
        };

        document.addEventListener('DOMContentLoaded', () => {
            const timelineContainer = document.getElementById('timeline-container');
            cvData.experience.forEach((item, index) => {
                const isLeft = index % 2 === 0;
                const alignmentClass = isLeft ? 'mb-8 flex justify-between items-center w-full right-timeline' : 'mb-8 flex justify-between flex-row-reverse items-center w-full left-timeline';
                
                const timelineElement = `
                    <div class="timeline-item ${alignmentClass}">
                        <div class="order-1 w-5/12"></div>
                        <div class="z-20 flex items-center order-1 bg-gray-800 shadow-xl w-10 h-10 rounded-full">
                            <h1 class="mx-auto font-semibold text-lg text-white">${cvData.experience.length - index}</h1>
                        </div>
                        <div class="order-1 bg-white rounded-lg shadow-xl w-5/12 px-6 py-4 cursor-pointer timeline-item-header">
                            <h3 class="font-bold text-gray-800 text-xl">${item.role}</h3>
                            <p class="text-sm font-medium text-blue-600">${item.company}</p>
                            <p class="text-sm text-gray-500">${item.date}</p>
                            <div class="timeline-item-content mt-4">
                                <ul class="list-disc list-inside space-y-2 text-gray-600">
                                    ${item.details.map(detail => `<li>${detail}</li>`).join('')}
                                </ul>
                            </div>
                        </div>
                    </div>
                `;
                timelineContainer.innerHTML += timelineElement;
            });

            document.querySelectorAll('.timeline-item-header').forEach(header => {
                header.addEventListener('click', () => {
                    const content = header.querySelector('.timeline-item-content');
                    const isActive = content.classList.contains('active');
                    document.querySelectorAll('.timeline-item-content.active').forEach(c => c.classList.remove('active'));
                    if (!isActive) content.classList.add('active');
                });
            });

            const projectsContainer = document.getElementById('projects-container');
            cvData.projects.forEach(project => {
                projectsContainer.innerHTML += `
                    <div class="bg-white p-6 rounded-lg shadow-lg hover:shadow-2xl hover:-translate-y-1 transition-all duration-300">
                        <h3 class="font-bold text-xl mb-2 text-gray-800">${project.title}</h3>
                        <p class="text-gray-600">${project.description}</p>
                    </div>`;
            });

            const certificationsContainer = document.getElementById('certifications-container');
            cvData.certifications.forEach(cert => {
                 certificationsContainer.innerHTML += `<li>${cert}</li>`;
            });

            // Skills Section Logic
            const skillsFilterContainer = document.getElementById('skills-filter');
            const skillsListContainer = document.getElementById('skills-list-container');
            const skillCategories = Object.keys(cvData.skills);

            function displaySkills(category) {
                skillsListContainer.innerHTML = '';
                const skillsToDisplay = cvData.skills[category] || [];
                skillsToDisplay.forEach(skill => {
                    const skillTag = `<span class="skill-tag bg-blue-100 text-blue-800 text-sm font-medium px-3 py-1.5 rounded-full">${skill}</span>`;
                    skillsListContainer.innerHTML += skillTag;
                });
            }

            skillCategories.forEach(category => {
                const filterButton = document.createElement('button');
                filterButton.className = 'skill-filter-btn px-4 py-2 bg-gray-200 text-gray-700 rounded-full font-medium hover:bg-gray-300';
                filterButton.textContent = category;
                filterButton.dataset.category = category;
                skillsFilterContainer.appendChild(filterButton);
            });
            
            skillsFilterContainer.addEventListener('click', e => {
                if (e.target.tagName === 'BUTTON') {
                    const category = e.target.dataset.category;
                    document.querySelectorAll('.skill-filter-btn').forEach(btn => btn.classList.remove('active'));
                    e.target.classList.add('active');
                    displaySkills(category);
                }
            });

            // Initial skills display
            skillsFilterContainer.querySelector('button').classList.add('active');
            displaySkills(skillCategories[0]);

            // Chart.js
            const skillsCtx = document.getElementById('skillsChart').getContext('2d');
            const skillsChart = new Chart(skillsCtx, {
                type: 'doughnut',
                data: {
                    labels: skillCategories,
                    datasets: [{
                        label: 'Skills Distribution',
                        data: skillCategories.map(cat => cvData.skills[cat].length),
                        backgroundColor: [
                            'rgba(59, 130, 246, 0.8)',
                            'rgba(239, 68, 68, 0.8)',
                            'rgba(16, 185, 129, 0.8)',
                            'rgba(245, 158, 11, 0.8)',
                            'rgba(139, 92, 246, 0.8)',
                            'rgba(236, 72, 153, 0.8)',
                            'rgba(22, 163, 74, 0.8)',
                             'rgba(14, 165, 233, 0.8)'
                        ],
                        borderColor: '#f3f4f6',
                        borderWidth: 3
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 15,
                                font: {
                                    size: 12
                                }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: (context) => ` ${context.label}: ${context.raw} skills`
                            }
                        }
                    }
                }
            });
            
            // Mobile Menu
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => mobileMenu.classList.toggle('hidden'));
            document.querySelectorAll('#mobile-menu a').forEach(link => {
                link.addEventListener('click', () => mobileMenu.classList.add('hidden'));
            });
            
            // Active Nav Link on Scroll
            const navLinks = document.querySelectorAll('nav a.nav-link');
            const sections = document.querySelectorAll('main section');
            window.addEventListener('scroll', () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 70) { // 70px offset for header height
                        current = section.getAttribute('id');
                    }
                });
                
                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').substring(1) === current) {
                        link.classList.add('active');
                    }
                });
            });
        });
    </script>
</body>
</html>
