# MERN-Stack-Development-mern-stack-integration-Edrisabdella
MERN-Stack-Development/mern-stack-integration-blog app development

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MERN Blog - Professional Blogging Platform</title>
    <meta name="description" content="Full-stack MERN blog application with authentication, CRUD operations, and advanced features">
    <meta name="author" content="Edris Abdella">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* Custom styles */
        .line-clamp-2 {
            overflow: hidden;
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 2;
        }
        
        .line-clamp-3 {
            overflow: hidden;
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 3;
        }
        
        .loading-spinner {
            display: inline-block;
            width: 50px;
            height: 50px;
            border: 3px solid #f3f4f6;
            border-radius: 50%;
            border-top-color: #3b82f6;
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease-in-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .slide-up {
            animation: slideUp 0.3s ease-out;
        }
        
        @keyframes slideUp {
            from { transform: translateY(10px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        /* Card hover effects */
        .card-hover {
            transition: all 0.3s ease;
        }
        
        .card-hover:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        
        /* Button animations */
        .btn-primary {
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(59, 130, 246, 0.4);
        }
        
        /* Rich text editor simulation */
        .rich-text-editor {
            min-height: 300px;
            border: 1px solid #d1d5db;
            border-radius: 0.5rem;
            padding: 1rem;
            background: white;
            font-family: 'Inter', sans-serif;
        }
        
        .rich-text-editor:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }
        
        /* Dark mode support */
        .dark-mode {
            background-color: #1f2937;
            color: #f9fafb;
        }
        
        .dark-mode .card {
            background-color: #374151;
            color: #f9fafb;
        }
        
        .dark-mode .text-gray-800 {
            color: #f9fafb;
        }
        
        .dark-mode .text-gray-600 {
            color: #d1d5db;
        }
        
        .dark-mode .border-gray-200 {
            border-color: #4b5563;
        }
        
        .dark-mode .bg-white {
            background-color: #374151;
        }
        
        .dark-mode .bg-gray-50 {
            background-color: #1f2937;
        }
        
        .dark-mode .bg-gray-100 {
            background-color: #374151;
        }
        
        .dark-mode input, 
        .dark-mode textarea, 
        .dark-mode select {
            background-color: #4b5563;
            color: #f9fafb;
            border-color: #6b7280;
        }
    </style>
</head>
<body class="bg-gray-50">
    <div id="app" class="min-h-screen flex flex-col"></div>

    <script>
        // MERN Blog Application - Single HTML File
        // Developed by Edris Abdella - Dire Dawa, Ethiopia
        
        // Mock Database
        const createMockDB = () => {
            // Initialize with sample data if not exists
            if (!localStorage.getItem('mern_blog_posts')) {
                const samplePosts = [
                    {
                        id: '1',
                        title: 'Welcome to MERN Blog',
                        content: 'This is a fully functional MERN stack blog application built with React, Node.js, Express, and MongoDB. It features user authentication, CRUD operations, and much more. This application demonstrates modern web development practices with a clean, responsive design.',
                        excerpt: 'Welcome to our MERN stack blog platform...',
                        featuredImage: '',
                        author: { id: '1', name: 'Edris Abdella' },
                        category: 'Technology',
                        tags: ['mern', 'react', 'nodejs'],
                        isPublished: true,
                        viewCount: 42,
                        comments: [
                            { id: '1', user: { name: 'John Doe' }, content: 'Great post! Looking forward to more content.', createdAt: new Date().toISOString() }
                        ],
                        createdAt: new Date().toISOString(),
                        updatedAt: new Date().toISOString()
                    },
                    {
                        id: '2',
                        title: 'Getting Started with React',
                        content: 'React is a powerful JavaScript library for building user interfaces. In this post, we will explore the fundamentals of React development including components, state, props, and hooks. React makes it painless to create interactive UIs with its component-based architecture.',
                        excerpt: 'Learn the basics of React development...',
                        featuredImage: '',
                        author: { id: '1', name: 'Edris Abdella' },
                        category: 'Programming',
                        tags: ['react', 'javascript', 'frontend'],
                        isPublished: true,
                        viewCount: 28,
                        comments: [],
                        createdAt: new Date(Date.now() - 86400000).toISOString(),
                        updatedAt: new Date(Date.now() - 86400000).toISOString()
                    },
                    {
                        id: '3',
                        title: 'Node.js Backend Development',
                        content: 'Node.js allows you to build scalable backend services with JavaScript. Learn how to create RESTful APIs with Express.js, connect to databases, handle authentication, and deploy your applications. Node.js has revolutionized backend development with its event-driven, non-blocking I/O model.',
                        excerpt: 'Building backend services with Node.js...',
                        featuredImage: '',
                        author: { id: '1', name: 'Edris Abdella' },
                        category: 'Backend',
                        tags: ['nodejs', 'express', 'backend'],
                        isPublished: true,
                        viewCount: 35,
                        comments: [],
                        createdAt: new Date(Date.now() - 172800000).toISOString(),
                        updatedAt: new Date(Date.now() - 172800000).toISOString()
                    },
                    {
                        id: '4',
                        title: 'MongoDB for Modern Applications',
                        content: 'MongoDB is a popular NoSQL database that provides flexibility and scalability for modern applications. In this article, we explore document-based data modeling, querying, aggregation pipelines, and best practices for using MongoDB in production environments.',
                        excerpt: 'Exploring MongoDB for modern applications...',
                        featuredImage: '',
                        author: { id: '1', name: 'Edris Abdella' },
                        category: 'Database',
                        tags: ['mongodb', 'database', 'nosql'],
                        isPublished: true,
                        viewCount: 19,
                        comments: [],
                        createdAt: new Date(Date.now() - 259200000).toISOString(),
                        updatedAt: new Date(Date.now() - 259200000).toISOString()
                    }
                ];
                localStorage.setItem('mern_blog_posts', JSON.stringify(samplePosts));
            }
            
            if (!localStorage.getItem('mern_blog_categories')) {
                const sampleCategories = [
                    { id: '1', name: 'Technology', description: 'Posts about technology and innovation' },
                    { id: '2', name: 'Programming', description: 'Coding tutorials and programming concepts' },
                    { id: '3', name: 'Backend', description: 'Server-side development and databases' },
                    { id: '4', name: 'Frontend', description: 'User interface and client-side development' },
                    { id: '5', name: 'Database', description: 'Database management and optimization' }
                ];
                localStorage.setItem('mern_blog_categories', JSON.stringify(sampleCategories));
            }
            
            return {
                // Posts operations
                posts: {
                    getAll: (page = 1, limit = 10, category = null) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        let filteredPosts = posts.filter(post => post.isPublished);
                        
                        if (category && category !== 'all') {
                            filteredPosts = filteredPosts.filter(post => post.category === category);
                        }
                        
                        const startIndex = (page - 1) * limit;
                        const endIndex = startIndex + limit;
                        const paginatedPosts = filteredPosts.slice(startIndex, endIndex);
                        
                        return {
                            posts: paginatedPosts,
                            pagination: {
                                page,
                                pages: Math.ceil(filteredPosts.length / limit),
                                total: filteredPosts.length
                            }
                        };
                    },
                    
                    getById: (id) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const post = posts.find(p => p.id === id);
                        
                        if (post) {
                            // Increment view count
                            post.viewCount += 1;
                            localStorage.setItem('mern_blog_posts', JSON.stringify(posts));
                        }
                        
                        return post;
                    },
                    
                    create: (postData) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const newPost = {
                            id: Date.now().toString(),
                            ...postData,
                            viewCount: 0,
                            comments: [],
                            createdAt: new Date().toISOString(),
                            updatedAt: new Date().toISOString()
                        };
                        
                        posts.unshift(newPost);
                        localStorage.setItem('mern_blog_posts', JSON.stringify(posts));
                        return newPost;
                    },
                    
                    update: (id, postData) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const index = posts.findIndex(p => p.id === id);
                        
                        if (index !== -1) {
                            posts[index] = {
                                ...posts[index],
                                ...postData,
                                updatedAt: new Date().toISOString()
                            };
                            localStorage.setItem('mern_blog_posts', JSON.stringify(posts));
                            return posts[index];
                        }
                        
                        return null;
                    },
                    
                    delete: (id) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const filteredPosts = posts.filter(p => p.id !== id);
                        localStorage.setItem('mern_blog_posts', JSON.stringify(filteredPosts));
                        return { success: true };
                    },
                    
                    search: (query) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const filteredPosts = posts.filter(post => 
                            post.title.toLowerCase().includes(query.toLowerCase()) ||
                            post.content.toLowerCase().includes(query.toLowerCase()) ||
                            post.excerpt.toLowerCase().includes(query.toLowerCase())
                        );
                        return filteredPosts;
                    },
                    
                    addComment: (postId, commentData) => {
                        const posts = JSON.parse(localStorage.getItem('mern_blog_posts') || '[]');
                        const post = posts.find(p => p.id === postId);
                        
                        if (post) {
                            const newComment = {
                                id: Date.now().toString(),
                                ...commentData,
                                createdAt: new Date().toISOString()
                            };
                            
                            post.comments.push(newComment);
                            localStorage.setItem('mern_blog_posts', JSON.stringify(posts));
                            return post.comments;
                        }
                        
                        return null;
                    }
                },
                
                // Categories operations
                categories: {
                    getAll: () => {
                        return JSON.parse(localStorage.getItem('mern_blog_categories') || '[]');
                    },
                    
                    create: (categoryData) => {
                        const categories = JSON.parse(localStorage.getItem('mern_blog_categories') || '[]');
                        const newCategory = {
                            id: Date.now().toString(),
                            ...categoryData
                        };
                        
                        categories.push(newCategory);
                        localStorage.setItem('mern_blog_categories', JSON.stringify(categories));
                        return newCategory;
                    }
                }
            };
        };

        // Utility functions
        const formatDate = (dateString) => {
            const date = new Date(dateString);
            return date.toLocaleDateString('en-US', {
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
        };

        const formatRelativeTime = (dateString) => {
            const date = new Date(dateString);
            const now = new Date();
            const diffInSeconds = Math.floor((now - date) / 1000);
            
            if (diffInSeconds < 60) {
                return 'just now';
            }
            
            const diffInMinutes = Math.floor(diffInSeconds / 60);
            if (diffInMinutes < 60) {
                return `${diffInMinutes} minute${diffInMinutes > 1 ? 's' : ''} ago`;
            }
            
            const diffInHours = Math.floor(diffInMinutes / 60);
            if (diffInHours < 24) {
                return `${diffInHours} hour${diffInHours > 1 ? 's' : ''} ago`;
            }
            
            const diffInDays = Math.floor(diffInHours / 24);
            if (diffInDays < 7) {
                return `${diffInDays} day${diffInDays > 1 ? 's' : ''} ago`;
            }
            
            return formatDate(dateString);
        };

        const generateExcerpt = (content, maxLength = 200) => {
            if (!content) return '';
            
            const plainText = content.replace(/<[^>]*>/g, '');
            
            if (plainText.length <= maxLength) {
                return plainText;
            }
            
            return plainText.substring(0, maxLength).trim() + '...';
        };

        // Router implementation
        const Router = {
            currentPath: '/',
            routes: {},
            
            init: function() {
                // Check for initial path
                const path = window.location.hash.replace('#', '') || '/';
                this.navigate(path, false);
                
                // Listen for hash changes
                window.addEventListener('hashchange', () => {
                    const path = window.location.hash.replace('#', '') || '/';
                    this.navigate(path, false);
                });
            },
            
            addRoute: function(path, component) {
                this.routes[path] = component;
            },
            
            navigate: function(path, updateHash = true) {
                this.currentPath = path;
                
                if (updateHash) {
                    window.location.hash = path;
                }
                
                if (this.routes[path]) {
                    this.routes[path]();
                } else {
                    // Check for dynamic routes (like /posts/:id)
                    const dynamicRoute = Object.keys(this.routes).find(route => {
                        const routePattern = route.replace(/:\w+/g, '([^\/]+)');
                        const regex = new RegExp(`^${routePattern}$`);
                        return regex.test(path);
                    });
                    
                    if (dynamicRoute) {
                        this.routes[dynamicRoute]();
                    } else {
                        // Show 404 page
                        this.show404();
                    }
                }
            },
            
            show404: function() {
                document.getElementById('app').innerHTML = `
                    <div class="min-h-screen bg-gray-50 flex items-center justify-center px-4 fade-in">
                        <div class="max-w-md w-full text-center">
                            <div class="bg-white rounded-lg shadow-lg p-8">
                                <div class="w-16 h-16 bg-red-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                    <i class="fas fa-exclamation-triangle text-red-600 text-2xl"></i>
                                </div>
                                <h2 class="text-2xl font-bold text-gray-800 mb-2">Page Not Found</h2>
                                <p class="text-gray-600 mb-6">
                                    The page you're looking for doesn't exist or has been moved.
                                </p>
                                <button onclick="Router.navigate('/')" class="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                                    Back to Home
                                </button>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            getParams: function() {
                const path = this.currentPath;
                const route = Object.keys(this.routes).find(route => {
                    const routePattern = route.replace(/:\w+/g, '([^\/]+)');
                    const regex = new RegExp(`^${routePattern}$`);
                    return regex.test(path);
                });
                
                if (!route) return {};
                
                const paramNames = [];
                const routePattern = route.replace(/:(\w+)/g, (match, paramName) => {
                    paramNames.push(paramName);
                    return '([^\/]+)';
                });
                
                const regex = new RegExp(`^${routePattern}$`);
                const matches = path.match(regex);
                
                const params = {};
                if (matches) {
                    paramNames.forEach((paramName, index) => {
                        params[paramName] = matches[index + 1];
                    });
                }
                
                return params;
            }
        };

        // State management
        const State = {
            user: null,
            darkMode: false,
            
            init: function() {
                // Load user from localStorage
                const storedUser = localStorage.getItem('mern_blog_user');
                if (storedUser) {
                    this.user = JSON.parse(storedUser);
                }
                
                // Load dark mode preference
                const storedDarkMode = localStorage.getItem('mern_blog_dark_mode');
                if (storedDarkMode) {
                    this.darkMode = JSON.parse(storedDarkMode);
                    this.toggleDarkMode(this.darkMode);
                }
                
                // Initialize mock database
                this.db = createMockDB();
            },
            
            setUser: function(user) {
                this.user = user;
                if (user) {
                    localStorage.setItem('mern_blog_user', JSON.stringify(user));
                } else {
                    localStorage.removeItem('mern_blog_user');
                }
            },
            
            toggleDarkMode: function(enable) {
                this.darkMode = enable !== undefined ? enable : !this.darkMode;
                localStorage.setItem('mern_blog_dark_mode', JSON.stringify(this.darkMode));
                
                if (this.darkMode) {
                    document.body.classList.add('dark-mode');
                } else {
                    document.body.classList.remove('dark-mode');
                }
            },
            
            logout: function() {
                this.setUser(null);
                Router.navigate('/');
            }
        };

        // Components
        const Components = {
            // Header Component
            Header: function() {
                const currentPath = Router.currentPath;
                const isActive = (path) => currentPath === path;
                
                return `
                    <header class="bg-white shadow-lg sticky top-0 z-50 transition-colors duration-200 dark-mode:bg-gray-800">
                        <div class="container mx-auto px-4 py-3">
                            <div class="flex items-center justify-between">
                                <!-- Logo -->
                                <a href="#/" class="flex items-center space-x-2 focus:outline-none focus:ring-2 focus:ring-blue-500 rounded-lg p-1">
                                    <div class="w-8 h-8 bg-gradient-to-r from-blue-600 to-purple-600 rounded-full flex items-center justify-center">
                                        <span class="text-white font-bold text-sm">MB</span>
                                    </div>
                                    <span class="text-xl font-bold text-gray-800 dark-mode:text-white">MERN Blog</span>
                                </a>

                                <!-- Desktop Navigation -->
                                <nav class="hidden md:flex items-center space-x-6">
                                    <a href="#/" class="${isActive('/') ? 'text-blue-600 font-medium' : 'text-gray-700 dark-mode:text-gray-300 hover:text-blue-600'} transition-colors duration-200">
                                        Home
                                    </a>
                                    <a href="#/posts" class="${isActive('/posts') ? 'text-blue-600 font-medium' : 'text-gray-700 dark-mode:text-gray-300 hover:text-blue-600'} transition-colors duration-200">
                                        Posts
                                    </a>
                                    
                                    <!-- Dark Mode Toggle -->
                                    <button onclick="State.toggleDarkMode()" class="p-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 rounded-lg">
                                        <i class="fas ${State.darkMode ? 'fa-sun' : 'fa-moon'}"></i>
                                    </button>
                                    
                                    ${State.user ? `
                                        <div class="flex items-center space-x-4">
                                            <a href="#/create-post" class="flex items-center space-x-1 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors duration-200">
                                                <i class="fas fa-edit"></i>
                                                <span>Write</span>
                                            </a>
                                            <div class="relative group">
                                                <button class="flex items-center space-x-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 rounded-lg p-2">
                                                    <i class="fas fa-user"></i>
                                                    <span>${State.user.name}</span>
                                                </button>
                                                <div class="absolute right-0 mt-2 w-48 bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg border border-gray-200 dark-mode:border-gray-700 opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 z-50">
                                                    <a href="#/profile" class="block px-4 py-2 text-gray-700 dark-mode:text-gray-300 hover:bg-gray-100 dark-mode:hover:bg-gray-700 transition-colors duration-200 rounded-t-lg">
                                                        Profile
                                                    </a>
                                                    <button onclick="State.logout()" class="flex items-center space-x-2 w-full px-4 py-2 text-gray-700 dark-mode:text-gray-300 hover:bg-gray-100 dark-mode:hover:bg-gray-700 transition-colors duration-200 rounded-b-lg text-left">
                                                        <i class="fas fa-sign-out-alt"></i>
                                                        <span>Logout</span>
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    ` : `
                                        <div class="flex items-center space-x-4">
                                            <a href="#/login" class="text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 font-medium transition-colors duration-200">
                                                Login
                                            </a>
                                            <a href="#/register" class="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors duration-200">
                                                Sign Up
                                            </a>
                                        </div>
                                    `}
                                </nav>

                                <!-- Mobile Menu Button -->
                                <button id="mobile-menu-button" class="md:hidden p-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 rounded-lg">
                                    <i class="fas fa-bars"></i>
                                </button>
                            </div>

                            <!-- Mobile Menu -->
                            <div id="mobile-menu" class="hidden md:hidden mt-4 pb-4 border-t border-gray-200 dark-mode:border-gray-700 pt-4">
                                <nav class="flex flex-col space-y-3">
                                    <a href="#/" class="font-medium py-2 ${isActive('/') ? 'text-blue-600' : 'text-gray-700 dark-mode:text-gray-300 hover:text-blue-600'} transition-colors duration-200">
                                        Home
                                    </a>
                                    <a href="#/posts" class="font-medium py-2 ${isActive('/posts') ? 'text-blue-600' : 'text-gray-700 dark-mode:text-gray-300 hover:text-blue-600'} transition-colors duration-200">
                                        Posts
                                    </a>
                                    
                                    <!-- Dark Mode Toggle - Mobile -->
                                    <button onclick="State.toggleDarkMode()" class="flex items-center space-x-2 font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200 text-left">
                                        <i class="fas ${State.darkMode ? 'fa-sun' : 'fa-moon'}"></i>
                                        <span>${State.darkMode ? 'Light Mode' : 'Dark Mode'}</span>
                                    </button>
                                    
                                    ${State.user ? `
                                        <a href="#/create-post" class="font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200">
                                            Write Post
                                        </a>
                                        <a href="#/profile" class="font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200">
                                            Profile
                                        </a>
                                        <button onclick="State.logout()" class="flex items-center space-x-2 font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200 text-left">
                                            <i class="fas fa-sign-out-alt"></i>
                                            <span>Logout</span>
                                        </button>
                                    ` : `
                                        <a href="#/login" class="font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200">
                                            Login
                                        </a>
                                        <a href="#/register" class="font-medium py-2 text-gray-700 dark-mode:text-gray-300 hover:text-blue-600 transition-colors duration-200">
                                            Sign Up
                                        </a>
                                    `}
                                </nav>
                            </div>
                        </div>
                    </header>
                `;
            },
            
            // Footer Component
            Footer: function() {
                return `
                    <footer class="bg-gray-800 text-white py-12 mt-auto">
                        <div class="container mx-auto px-4">
                            <div class="grid md:grid-cols-4 gap-8">
                                <div>
                                    <div class="flex items-center space-x-2 mb-4">
                                        <div class="w-8 h-8 bg-gradient-to-r from-blue-600 to-purple-600 rounded-full flex items-center justify-center">
                                            <span class="text-white font-bold text-sm">MB</span>
                                        </div>
                                        <span class="text-xl font-bold">MERN Blog</span>
                                    </div>
                                    <p class="text-gray-400 mb-4">
                                        A professional blogging platform built with the MERN stack. Share your stories with the world.
                                    </p>
                                    <div class="flex space-x-4">
                                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                                            <i class="fab fa-twitter"></i>
                                        </a>
                                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                                            <i class="fab fa-facebook"></i>
                                        </a>
                                        <a href="#" class="text-gray-400 hover:text-white transition-colors">
                                            <i class="fab fa-linkedin"></i>
                                        </a>
                                    </div>
                                </div>
                                
                                <div>
                                    <h3 class="text-lg font-semibold mb-4">Quick Links</h3>
                                    <ul class="space-y-2">
                                        <li><a href="#/" class="text-gray-400 hover:text-white transition-colors">Home</a></li>
                                        <li><a href="#/posts" class="text-gray-400 hover:text-white transition-colors">All Posts</a></li>
                                        <li><a href="#/create-post" class="text-gray-400 hover:text-white transition-colors">Write a Post</a></li>
                                    </ul>
                                </div>
                                
                                <div>
                                    <h3 class="text-lg font-semibold mb-4">Categories</h3>
                                    <ul class="space-y-2">
                                        <li><a href="#/posts?category=Technology" class="text-gray-400 hover:text-white transition-colors">Technology</a></li>
                                        <li><a href="#/posts?category=Programming" class="text-gray-400 hover:text-white transition-colors">Programming</a></li>
                                        <li><a href="#/posts?category=Backend" class="text-gray-400 hover:text-white transition-colors">Backend</a></li>
                                        <li><a href="#/posts?category=Frontend" class="text-gray-400 hover:text-white transition-colors">Frontend</a></li>
                                    </ul>
                                </div>
                                
                                <div>
                                    <h3 class="text-lg font-semibold mb-4">Contact Info</h3>
                                    <div class="space-y-2 text-gray-400">
                                        <p>Developed by <strong class="text-white">Edris Abdella</strong></p>
                                        <p><i class="fas fa-map-marker-alt mr-2"></i>Dire Dawa, Ethiopia</p>
                                        <p><i class="fas fa-envelope mr-2"></i>edrisabdella178@gmail.com</p>
                                        <p><i class="fas fa-phone mr-2"></i>+251944676746 | +251905131051</p>
                                        <div class="pt-2">
                                            <a href="https://www.linkedin.com/in/edris-abdella-7aa521177" class="text-blue-400 hover:text-blue-300 transition-colors">
                                                <i class="fab fa-linkedin mr-1"></i>LinkedIn Profile
                                            </a>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
                                <p>&copy; 2024 MERN Blog. All rights reserved. Built with <i class="fas fa-heart text-red-500"></i> by Edris Abdella</p>
                            </div>
                        </div>
                    </footer>
                `;
            },
            
            // Home Page Component
            Home: function() {
                const postsData = State.db.posts.getAll(1, 6);
                const featuredPosts = postsData.posts.slice(0, 3);
                const recentPosts = postsData.posts;
                
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 fade-in">
                        <!-- Hero Section -->
                        <section class="bg-gradient-to-r from-blue-600 to-purple-700 text-white py-20">
                            <div class="container mx-auto px-4 text-center">
                                <h1 class="text-4xl md:text-5xl font-bold mb-6">Welcome to MERN Blog</h1>
                                <p class="text-xl mb-8 max-w-2xl mx-auto">
                                    Discover amazing stories, technical insights, and creative ideas from our community of writers.
                                </p>
                                <div class="flex flex-col sm:flex-row gap-4 justify-center">
                                    <a href="#/posts" class="bg-white text-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition-colors btn-primary">
                                        Explore Posts
                                    </a>
                                    <a href="#/register" class="border-2 border-white text-white px-8 py-3 rounded-lg font-semibold hover:bg-white hover:text-blue-600 transition-colors">
                                        Start Writing
                                    </a>
                                </div>
                            </div>
                        </section>

                        <!-- Featured Posts -->
                        <section class="py-16">
                            <div class="container mx-auto px-4">
                                <h2 class="text-3xl font-bold text-gray-800 dark-mode:text-white mb-8 text-center">Featured Posts</h2>
                                <div class="grid md:grid-cols-3 gap-8">
                                    ${featuredPosts.map(post => `
                                        <article class="bg-white dark-mode:bg-gray-800 rounded-xl shadow-lg overflow-hidden hover:shadow-xl transition-shadow slide-up card-hover">
                                            <div class="p-6">
                                                <div class="flex items-center text-sm text-gray-600 dark-mode:text-gray-400 mb-3">
                                                    <i class="far fa-calendar mr-1"></i>
                                                    <span>${formatDate(post.createdAt)}</span>
                                                    <span class="mx-2">•</span>
                                                    <i class="far fa-eye mr-1"></i>
                                                    <span>${post.viewCount} views</span>
                                                </div>
                                                <h3 class="text-xl font-bold text-gray-800 dark-mode:text-white mb-3 line-clamp-2">
                                                    ${post.title}
                                                </h3>
                                                <p class="text-gray-600 dark-mode:text-gray-300 mb-4 line-clamp-3">
                                                    ${post.excerpt || generateExcerpt(post.content, 150)}
                                                </p>
                                                <div class="flex items-center justify-between">
                                                    <div class="flex items-center text-sm text-gray-600 dark-mode:text-gray-400">
                                                        <i class="far fa-user mr-1"></i>
                                                        <span>${post.author?.name}</span>
                                                    </div>
                                                    <a href="#/posts/${post.id}" class="flex items-center text-blue-600 hover:text-blue-700 font-medium">
                                                        Read More
                                                        <i class="fas fa-arrow-right ml-1"></i>
                                                    </a>
                                                </div>
                                            </div>
                                        </article>
                                    `).join('')}
                                </div>
                            </div>
                        </section>

                        <!-- Recent Posts -->
                        <section class="py-16 bg-white dark-mode:bg-gray-800">
                            <div class="container mx-auto px-4">
                                <div class="flex justify-between items-center mb-8">
                                    <h2 class="text-3xl font-bold text-gray-800 dark-mode:text-white">Recent Posts</h2>
                                    <a href="#/posts" class="text-blue-600 hover:text-blue-700 font-medium">
                                        View All Posts
                                    </a>
                                </div>
                                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                                    ${recentPosts.map(post => `
                                        <article class="bg-gray-50 dark-mode:bg-gray-700 rounded-lg p-6 hover:shadow-md transition-shadow slide-up card-hover">
                                            <h3 class="text-lg font-bold text-gray-800 dark-mode:text-white mb-3 line-clamp-2">
                                                ${post.title}
                                            </h3>
                                            <p class="text-gray-600 dark-mode:text-gray-300 mb-4 line-clamp-3">
                                                ${post.excerpt || generateExcerpt(post.content, 120)}
                                            </p>
                                            <div class="flex items-center justify-between text-sm text-gray-500 dark-mode:text-gray-400">
                                                <span>${post.author?.name}</span>
                                                <span>${formatDate(post.createdAt)}</span>
                                            </div>
                                            <a href="#/posts/${post.id}" class="mt-4 inline-block text-blue-600 hover:text-blue-700 font-medium">
                                                Read More →
                                            </a>
                                        </article>
                                    `).join('')}
                                </div>
                            </div>
                        </section>

                        <!-- CTA Section -->
                        <section class="py-16 bg-gray-800 text-white">
                            <div class="container mx-auto px-4 text-center">
                                <h2 class="text-3xl font-bold mb-4">Ready to Share Your Story?</h2>
                                <p class="text-xl mb-8 max-w-2xl mx-auto">
                                    Join our community of writers and start sharing your ideas with the world.
                                </p>
                                <a href="#/register" class="bg-blue-600 text-white px-8 py-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors btn-primary">
                                    Get Started Today
                                </a>
                            </div>
                        </section>
                    </div>
                `;
            },
            
            // Posts Page Component
            Posts: function() {
                const urlParams = new URLSearchParams(window.location.hash.split('?')[1]);
                const category = urlParams.get('category') || 'all';
                const page = parseInt(urlParams.get('page')) || 1;
                
                const postsData = State.db.posts.getAll(page, 6, category === 'all' ? null : category);
                const categories = State.db.categories.getAll();
                
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 py-8 fade-in">
                        <div class="container mx-auto px-4">
                            <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8">
                                <h1 class="text-3xl font-bold text-gray-800 dark-mode:text-white mb-4 md:mb-0">All Blog Posts</h1>
                                
                                <div class="flex flex-col sm:flex-row gap-4">
                                    <select onchange="window.location.href='#/posts?category=' + this.value" 
                                        class="px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg bg-white dark-mode:bg-gray-800 text-gray-900 dark-mode:text-white focus:outline-none focus:ring-2 focus:ring-blue-500">
                                        <option value="all" ${category === 'all' ? 'selected' : ''}>All Categories</option>
                                        ${categories.map(cat => `
                                            <option value="${cat.name}" ${category === cat.name ? 'selected' : ''}>${cat.name}</option>
                                        `).join('')}
                                    </select>
                                    
                                    ${State.user ? `
                                        <a href="#/create-post" class="flex items-center space-x-1 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors btn-primary">
                                            <i class="fas fa-plus"></i>
                                            <span>New Post</span>
                                        </a>
                                    ` : ''}
                                </div>
                            </div>
                            
                            ${postsData.posts.length === 0 ? `
                                <div class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-md p-8 text-center">
                                    <h3 class="text-xl font-semibold text-gray-800 dark-mode:text-white mb-2">No posts found</h3>
                                    <p class="text-gray-600 dark-mode:text-gray-400 mb-4">
                                        ${category !== 'all' 
                                            ? `No posts found in the ${category} category.` 
                                            : 'No posts have been published yet.'}
                                    </p>
                                    ${category !== 'all' ? `
                                        <button onclick="Router.navigate('/posts')" class="text-blue-600 hover:text-blue-700 font-medium">
                                            View all posts
                                        </button>
                                    ` : ''}
                                </div>
                            ` : `
                                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                                    ${postsData.posts.map(post => `
                                        <article class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow slide-up card-hover">
                                            <div class="p-6">
                                                <div class="flex items-center justify-between text-sm text-gray-600 dark-mode:text-gray-400 mb-3">
                                                    <span class="bg-blue-100 dark-mode:bg-blue-900 text-blue-800 dark-mode:text-blue-200 px-2 py-1 rounded">
                                                        ${post.category}
                                                    </span>
                                                    <div class="flex items-center">
                                                        <i class="far fa-eye mr-1"></i>
                                                        <span>${post.viewCount}</span>
                                                    </div>
                                                </div>
                                                
                                                <h2 class="text-xl font-bold text-gray-800 dark-mode:text-white mb-3 line-clamp-2">
                                                    ${post.title}
                                                </h2>
                                                
                                                <p class="text-gray-600 dark-mode:text-gray-300 mb-4 line-clamp-3">
                                                    ${post.excerpt || generateExcerpt(post.content, 120)}
                                                </p>
                                                
                                                <div class="flex items-center justify-between">
                                                    <div class="flex items-center text-sm text-gray-500 dark-mode:text-gray-400">
                                                        <i class="far fa-user mr-1"></i>
                                                        <span>${post.author?.name}</span>
                                                        <span class="mx-2">•</span>
                                                        <i class="far fa-calendar mr-1"></i>
                                                        <span>${formatDate(post.createdAt)}</span>
                                                    </div>
                                                    
                                                    <a href="#/posts/${post.id}" class="text-blue-600 hover:text-blue-700 font-medium">
                                                        Read More
                                                    </a>
                                                </div>
                                            </div>
                                        </article>
                                    `).join('')}
                                </div>
                            `}
                            
                            <!-- Pagination -->
                            <div class="flex justify-center mt-12">
                                <div class="flex space-x-2">
                                    <button onclick="Router.navigate('/posts?category=${category}&page=${page - 1}')" 
                                        ${page === 1 ? 'disabled' : ''}
                                        class="px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg bg-white dark-mode:bg-gray-800 text-gray-700 dark-mode:text-gray-300 hover:bg-gray-50 dark-mode:hover:bg-gray-700 disabled:opacity-50 disabled:cursor-not-allowed">
                                        Previous
                                    </button>
                                    
                                    <span class="px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg bg-white dark-mode:bg-gray-800 text-gray-700 dark-mode:text-gray-300">
                                        Page ${page} of ${postsData.pagination.pages}
                                    </span>
                                    
                                    <button onclick="Router.navigate('/posts?category=${category}&page=${page + 1}')" 
                                        ${page >= postsData.pagination.pages ? 'disabled' : ''}
                                        class="px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg bg-white dark-mode:bg-gray-800 text-gray-700 dark-mode:text-gray-300 hover:bg-gray-50 dark-mode:hover:bg-gray-700 disabled:opacity-50 disabled:cursor-not-allowed">
                                        Next
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            // Single Post Page Component
            Post: function() {
                const params = Router.getParams();
                const postId = params.id;
                const post = State.db.posts.getById(postId);
                
                if (!post) {
                    return `
                        <div class="min-h-screen flex items-center justify-center">
                            <div class="text-center">
                                <h2 class="text-2xl font-bold text-gray-800 dark-mode:text-white mb-4">Post Not Found</h2>
                                <p class="text-gray-600 dark-mode:text-gray-400 mb-6">The post you're looking for doesn't exist.</p>
                                <a href="#/posts" class="text-blue-600 hover:text-blue-700 font-medium">
                                    Back to All Posts
                                </a>
                            </div>
                        </div>
                    `;
                }
                
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 py-8 fade-in">
                        <div class="container mx-auto px-4 max-w-4xl">
                            <article class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg overflow-hidden">
                                <!-- Post Header -->
                                <div class="p-8 border-b border-gray-200 dark-mode:border-gray-700">
                                    <div class="flex flex-wrap items-center justify-between mb-4">
                                        <span class="bg-blue-100 dark-mode:bg-blue-900 text-blue-800 dark-mode:text-blue-200 px-3 py-1 rounded-full text-sm font-medium">
                                            ${post.category}
                                        </span>
                                        <div class="flex items-center space-x-4 text-sm text-gray-600 dark-mode:text-gray-400">
                                            <div class="flex items-center">
                                                <i class="far fa-eye mr-1"></i>
                                                <span>${post.viewCount} views</span>
                                            </div>
                                            <div class="flex items-center">
                                                <i class="far fa-comment mr-1"></i>
                                                <span>${post.comments.length} comments</span>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <h1 class="text-3xl md:text-4xl font-bold text-gray-800 dark-mode:text-white mb-4">
                                        ${post.title}
                                    </h1>
                                    
                                    <div class="flex items-center justify-between">
                                        <div class="flex items-center space-x-4">
                                            <div class="w-10 h-10 bg-blue-600 rounded-full flex items-center justify-center">
                                                <span class="text-white font-semibold">
                                                    ${post.author?.name?.charAt(0) || 'U'}
                                                </span>
                                            </div>
                                            <div>
                                                <p class="font-medium text-gray-800 dark-mode:text-white">${post.author?.name}</p>
                                                <p class="text-sm text-gray-600 dark-mode:text-gray-400">
                                                    ${formatDate(post.createdAt)}
                                                </p>
                                            </div>
                                        </div>
                                        
                                        <div class="flex space-x-2">
                                            <button class="p-2 text-gray-600 dark-mode:text-gray-400 hover:text-blue-600 dark-mode:hover:text-blue-400 transition-colors">
                                                <i class="fas fa-share"></i>
                                            </button>
                                            <button class="p-2 text-gray-600 dark-mode:text-gray-400 hover:text-blue-600 dark-mode:hover:text-blue-400 transition-colors">
                                                <i class="far fa-bookmark"></i>
                                            </button>
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- Post Content -->
                                <div class="p-8">
                                    <div class="prose dark-mode:prose-invert max-w-none">
                                        <p class="text-gray-700 dark-mode:text-gray-300 leading-relaxed whitespace-pre-line">
                                            ${post.content}
                                        </p>
                                    </div>
                                    
                                    <!-- Tags -->
                                    ${post.tags && post.tags.length > 0 ? `
                                        <div class="mt-8 pt-6 border-t border-gray-200 dark-mode:border-gray-700">
                                            <div class="flex flex-wrap gap-2">
                                                ${post.tags.map(tag => `
                                                    <span class="bg-gray-100 dark-mode:bg-gray-700 text-gray-800 dark-mode:text-gray-200 px-3 py-1 rounded-full text-sm">
                                                        #${tag}
                                                    </span>
                                                `).join('')}
                                            </div>
                                        </div>
                                    ` : ''}
                                </div>
                                
                                <!-- Comments Section -->
                                <div class="p-8 border-t border-gray-200 dark-mode:border-gray-700">
                                    <h3 class="text-xl font-bold text-gray-800 dark-mode:text-white mb-6">
                                        Comments (${post.comments.length})
                                    </h3>
                                    
                                    <!-- Add Comment Form -->
                                    ${State.user ? `
                                        <form onsubmit="handleAddComment(event, '${post.id}')" class="mb-8">
                                            <div class="flex space-x-4">
                                                <div class="w-10 h-10 bg-blue-600 rounded-full flex items-center justify-center flex-shrink-0">
                                                    <span class="text-white font-semibold">
                                                        ${State.user.name.charAt(0)}
                                                    </span>
                                                </div>
                                                <div class="flex-1">
                                                    <textarea id="comment-content" placeholder="Add a comment..." rows="3"
                                                        class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white resize-none" required></textarea>
                                                    <div class="flex justify-end mt-2">
                                                        <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                                                            Post Comment
                                                        </button>
                                                    </div>
                                                </div>
                                            </div>
                                        </form>
                                    ` : `
                                        <div class="bg-gray-100 dark-mode:bg-gray-700 rounded-lg p-4 text-center mb-8">
                                            <p class="text-gray-700 dark-mode:text-gray-300">
                                                Please <a href="#/login" class="text-blue-600 hover:text-blue-700">login</a> to add a comment.
                                            </p>
                                        </div>
                                    `}
                                    
                                    <!-- Comments List -->
                                    <div class="space-y-6">
                                        ${post.comments.length === 0 ? `
                                            <p class="text-gray-600 dark-mode:text-gray-400 text-center py-4">
                                                No comments yet. Be the first to comment!
                                            </p>
                                        ` : post.comments.map(comment => `
                                            <div class="flex space-x-4">
                                                <div class="w-10 h-10 bg-gray-300 dark-mode:bg-gray-600 rounded-full flex items-center justify-center flex-shrink-0">
                                                    <span class="text-gray-700 dark-mode:text-gray-300 font-semibold">
                                                        ${comment.user.name.charAt(0)}
                                                    </span>
                                                </div>
                                                <div class="flex-1">
                                                    <div class="bg-gray-100 dark-mode:bg-gray-700 rounded-lg p-4">
                                                        <div class="flex items-center justify-between mb-2">
                                                            <p class="font-medium text-gray-800 dark-mode:text-white">
                                                                ${comment.user.name}
                                                            </p>
                                                            <p class="text-sm text-gray-600 dark-mode:text-gray-400">
                                                                ${formatRelativeTime(comment.createdAt)}
                                                            </p>
                                                        </div>
                                                        <p class="text-gray-700 dark-mode:text-gray-300">
                                                            ${comment.content}
                                                        </p>
                                                    </div>
                                                </div>
                                            </div>
                                        `).join('')}
                                    </div>
                                </div>
                            </article>
                            
                            <!-- Back to Posts -->
                            <div class="mt-8 text-center">
                                <a href="#/posts" class="inline-flex items-center text-blue-600 hover:text-blue-700 font-medium">
                                    <i class="fas fa-arrow-left mr-2"></i>
                                    Back to All Posts
                                </a>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            // Create Post Component
            CreatePost: function() {
                if (!State.user) {
                    setTimeout(() => Router.navigate('/login'), 0);
                    return '<div class="min-h-screen flex items-center justify-center"><div class="loading-spinner"></div></div>';
                }
                
                const categories = State.db.categories.getAll();
                
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 py-8 fade-in">
                        <div class="container mx-auto px-4 max-w-4xl">
                            <div class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg overflow-hidden">
                                <div class="p-6 border-b border-gray-200 dark-mode:border-gray-700">
                                    <h1 class="text-2xl font-bold text-gray-800 dark-mode:text-white">Create New Post</h1>
                                    <p class="text-gray-600 dark-mode:text-gray-400 mt-2">
                                        Share your thoughts and ideas with the community
                                    </p>
                                </div>
                                
                                <form onsubmit="handleCreatePost(event)" class="p-6 space-y-6">
                                    <!-- Title -->
                                    <div>
                                        <label for="post-title" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Post Title *
                                        </label>
                                        <input type="text" id="post-title" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter a compelling title for your post">
                                    </div>
                                    
                                    <!-- Category -->
                                    <div>
                                        <label for="post-category" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Category *
                                        </label>
                                        <select id="post-category" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white">
                                            <option value="">Select a category</option>
                                            ${categories.map(cat => `
                                                <option value="${cat.name}">${cat.name}</option>
                                            `).join('')}
                                        </select>
                                    </div>
                                    
                                    <!-- Tags -->
                                    <div>
                                        <label for="post-tags" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Tags
                                        </label>
                                        <input type="text" id="post-tags"
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Separate tags with commas (e.g., react, javascript, web)">
                                        <p class="text-sm text-gray-500 dark-mode:text-gray-400 mt-1">
                                            Separate multiple tags with commas
                                        </p>
                                    </div>
                                    
                                    <!-- Content -->
                                    <div>
                                        <label for="post-content" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Content *
                                        </label>
                                        <textarea id="post-content" rows="15" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white resize-none rich-text-editor"
                                            placeholder="Write your post content here..."></textarea>
                                    </div>
                                    
                                    <!-- Publish Option -->
                                    <div class="flex items-center">
                                        <input type="checkbox" id="post-published" checked
                                            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500">
                                        <label for="post-published" class="ml-2 text-sm font-medium text-gray-700 dark-mode:text-gray-300">
                                            Publish immediately
                                        </label>
                                    </div>
                                    
                                    <!-- Submit Buttons -->
                                    <div class="flex justify-end space-x-4 pt-6 border-t border-gray-200 dark-mode:border-gray-700">
                                        <a href="#/posts" class="px-6 py-2 border border-gray-300 dark-mode:border-gray-600 text-gray-700 dark-mode:text-gray-300 rounded-lg hover:bg-gray-50 dark-mode:hover:bg-gray-700 transition-colors">
                                            Cancel
                                        </a>
                                        <button type="submit" class="px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors btn-primary">
                                            Publish Post
                                        </button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            // Login Component
            Login: function() {
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 flex items-center justify-center py-12 px-4 fade-in">
                        <div class="max-w-md w-full space-y-8">
                            <div class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg p-8">
                                <div class="text-center">
                                    <div class="mx-auto w-16 h-16 bg-gradient-to-r from-blue-600 to-purple-600 rounded-full flex items-center justify-center mb-4">
                                        <span class="text-white font-bold text-xl">MB</span>
                                    </div>
                                    <h2 class="text-3xl font-bold text-gray-800 dark-mode:text-white">Sign in to your account</h2>
                                    <p class="mt-2 text-gray-600 dark-mode:text-gray-400">
                                        Or <a href="#/register" class="font-medium text-blue-600 hover:text-blue-500">create a new account</a>
                                    </p>
                                </div>
                                
                                <form onsubmit="handleLogin(event)" class="mt-8 space-y-6">
                                    <div id="login-error" class="hidden bg-red-50 dark-mode:bg-red-900/20 border border-red-200 dark-mode:border-red-800 rounded-lg p-4">
                                        <p class="text-red-800 dark-mode:text-red-200 text-sm" id="login-error-text"></p>
                                    </div>
                                    
                                    <div>
                                        <label for="login-email" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Email address
                                        </label>
                                        <input id="login-email" name="email" type="email" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter your email">
                                    </div>
                                    
                                    <div>
                                        <label for="login-password" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Password
                                        </label>
                                        <input id="login-password" name="password" type="password" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter your password">
                                    </div>
                                    
                                    <div>
                                        <button type="submit" class="group relative w-full flex justify-center py-3 px-4 border border-transparent text-sm font-medium rounded-lg text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-colors btn-primary">
                                            Sign in
                                        </button>
                                    </div>
                                    
                                    <div class="text-center">
                                        <p class="text-gray-600 dark-mode:text-gray-400 text-sm">
                                            Demo: Use any email and password to login
                                        </p>
                                    </div>
                                </form>
                            </div>
                            
                            <div class="text-center">
                                <p class="text-gray-600 dark-mode:text-gray-400 text-sm">
                                    Developed by <strong class="text-gray-800 dark-mode:text-white">Edris Abdella</strong>
                                </p>
                                <p class="text-gray-500 dark-mode:text-gray-500 text-xs mt-1">
                                    <i class="fas fa-map-marker-alt mr-1"></i>Dire Dawa, Ethiopia | 
                                    <i class="fas fa-envelope mr-1"></i>edrisabdella178@gmail.com
                                </p>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            // Register Component
            Register: function() {
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 flex items-center justify-center py-12 px-4 fade-in">
                        <div class="max-w-md w-full space-y-8">
                            <div class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg p-8">
                                <div class="text-center">
                                    <div class="mx-auto w-16 h-16 bg-gradient-to-r from-blue-600 to-purple-600 rounded-full flex items-center justify-center mb-4">
                                        <span class="text-white font-bold text-xl">MB</span>
                                    </div>
                                    <h2 class="text-3xl font-bold text-gray-800 dark-mode:text-white">Create your account</h2>
                                    <p class="mt-2 text-gray-600 dark-mode:text-gray-400">
                                        Or <a href="#/login" class="font-medium text-blue-600 hover:text-blue-500">sign in to existing account</a>
                                    </p>
                                </div>
                                
                                <form onsubmit="handleRegister(event)" class="mt-8 space-y-6">
                                    <div id="register-error" class="hidden bg-red-50 dark-mode:bg-red-900/20 border border-red-200 dark-mode:border-red-800 rounded-lg p-4">
                                        <p class="text-red-800 dark-mode:text-red-200 text-sm" id="register-error-text"></p>
                                    </div>
                                    
                                    <div>
                                        <label for="register-name" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Full Name
                                        </label>
                                        <input id="register-name" name="name" type="text" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter your full name">
                                    </div>
                                    
                                    <div>
                                        <label for="register-email" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Email address
                                        </label>
                                        <input id="register-email" name="email" type="email" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter your email">
                                    </div>
                                    
                                    <div>
                                        <label for="register-password" class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-2">
                                            Password
                                        </label>
                                        <input id="register-password" name="password" type="password" required
                                            class="w-full px-4 py-2 border border-gray-300 dark-mode:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white dark-mode:bg-gray-700 text-gray-900 dark-mode:text-white"
                                            placeholder="Enter your password">
                                    </div>
                                    
                                    <div>
                                        <button type="submit" class="group relative w-full flex justify-center py-3 px-4 border border-transparent text-sm font-medium rounded-lg text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-colors btn-primary">
                                            Create account
                                        </button>
                                    </div>
                                </form>
                            </div>
                            
                            <div class="text-center">
                                <p class="text-gray-600 dark-mode:text-gray-400 text-sm">
                                    Developed by <strong class="text-gray-800 dark-mode:text-white">Edris Abdella</strong>
                                </p>
                                <p class="text-gray-500 dark-mode:text-gray-500 text-xs mt-1">
                                    <i class="fas fa-map-marker-alt mr-1"></i>Dire Dawa, Ethiopia | 
                                    <i class="fas fa-envelope mr-1"></i>edrisabdella178@gmail.com
                                </p>
                            </div>
                        </div>
                    </div>
                `;
            },
            
            // Profile Component
            Profile: function() {
                if (!State.user) {
                    setTimeout(() => Router.navigate('/login'), 0);
                    return '<div class="min-h-screen flex items-center justify-center"><div class="loading-spinner"></div></div>';
                }
                
                return `
                    <div class="min-h-screen bg-gray-50 dark-mode:bg-gray-900 py-8 fade-in">
                        <div class="container mx-auto px-4 max-w-4xl">
                            <div class="bg-white dark-mode:bg-gray-800 rounded-lg shadow-lg overflow-hidden">
                                <div class="p-6 border-b border-gray-200 dark-mode:border-gray-700">
                                    <h1 class="text-2xl font-bold text-gray-800 dark-mode:text-white">User Profile</h1>
                                    <p class="text-gray-600 dark-mode:text-gray-400 mt-2">
                                        Manage your account information
                                    </p>
                                </div>
                                
                                <div class="p-6">
                                    <div class="flex flex-col md:flex-row items-start space-y-6 md:space-y-0 md:space-x-6">
                                        <!-- Avatar -->
                                        <div class="flex-shrink-0">
                                            <div class="w-24 h-24 bg-gradient-to-r from-blue-600 to-purple-600 rounded-full flex items-center justify-center">
                                                <span class="text-white font-bold text-2xl">
                                                    ${State.user.name.charAt(0).toUpperCase()}
                                                </span>
                                            </div>
                                        </div>
                                        
                                        <!-- User Info -->
                                        <div class="flex-1 space-y-4">
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-1">
                                                    Full Name
                                                </label>
                                                <p class="text-gray-900 dark-mode:text-white text-lg font-semibold">
                                                    ${State.user.name}
                                                </p>
                                            </div>
                                            
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-1">
                                                    Email Address
                                                </label>
                                                <p class="text-gray-900 dark-mode:text-white text-lg">
                                                    ${State.user.email}
                                                </p>
                                            </div>
                                            
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-1">
                                                    Account Role
                                                </label>
                                                <p class="text-gray-900 dark-mode:text-white text-lg">
                                                    ${State.user.role.charAt(0).toUpperCase() + State.user.role.slice(1)}
                                                </p>
                                            </div>
                                            
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 dark-mode:text-gray-300 mb-1">
                                                    Member Since
                                                </label>
                                                <p class="text-gray-900 dark-mode:text-white text-lg">
                                                    ${formatDate(new Date().toISOString())}
                                                </p>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Developer Info -->
                                    <div class="mt-8 pt-6 border-t border-gray-200 dark-mode:border-gray-700">
                                        <h3 class="text-lg font-semibold text-gray-800 dark-mode:text-white mb-4">
                                            About the Developer
                                        </h3>
                                        <div class="bg-blue-50 dark-mode:bg-blue-900/20 rounded-lg p-4">
                                            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between">
                                                <div>
                                                    <p class="font-medium text-blue-800 dark-mode:text-blue-200">
                                                        Edris Abdella
                                                    </p>
                                                    <p class="text-blue-700 dark-mode:text-blue-300 text-sm">
                                                        Full Stack Developer
                                                    </p>
                                                    <div class="mt-2 space-y-1 text-sm text-blue-600 dark-mode:text-blue-400">
                                                        <p><i class="fas fa-map-marker-alt mr-2"></i>Dire Dawa, Ethiopia</p>
                                                        <p><i class="fas fa-envelope mr-2"></i>edrisabdella178@gmail.com</p>
                                                        <p><i class="fas fa-phone mr-2"></i>+251944676746 | +251905131051</p>
                                                    </div>
                                                </div>
                                                <div class="mt-4 sm:mt-0">
                                                    <a href="https://www.linkedin.com/in/edris-abdella-7aa521177" target="_blank"
                                                        class="inline-flex items-center text-blue-600 hover:text-blue-700 font-medium">
                                                        LinkedIn Profile
                                                        <i class="fas fa-external-link-alt ml-1"></i>
                                                    </a>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }
        };

        // Event Handlers
        function handleLogin(event) {
            event.preventDefault();
            
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            
            // Simple validation
            if (!email || !password) {
                showError('login-error', 'Please fill in all fields');
                return;
            }
            
            // Simulate API call
            setTimeout(() => {
                const userData = {
                    id: '1',
                    name: email.split('@')[0],
                    email: email,
                    role: 'user'
                };
                
                State.setUser(userData);
                Router.navigate('/');
            }, 500);
        }
        
        function handleRegister(event) {
            event.preventDefault();
            
            const name = document.getElementById('register-name').value;
            const email = document.getElementById('register-email').value;
            const password = document.getElementById('register-password').value;
            
            // Simple validation
            if (!name || !email || !password) {
                showError('register-error', 'Please fill in all fields');
                return;
            }
            
            if (password.length < 6) {
                showError('register-error', 'Password must be at least 6 characters');
                return;
            }
            
            // Simulate API call
            setTimeout(() => {
                const userData = {
                    id: Date.now().toString(),
                    name: name,
                    email: email,
                    role: 'user'
                };
                
                State.setUser(userData);
                Router.navigate('/');
            }, 500);
        }
        
        function handleCreatePost(event) {
            event.preventDefault();
            
            const title = document.getElementById('post-title').value;
            const category = document.getElementById('post-category').value;
            const tags = document.getElementById('post-tags').value;
            const content = document.getElementById('post-content').value;
            const isPublished = document.getElementById('post-published').checked;
            
            // Validation
            if (!title || !category || !content) {
                alert('Please fill in all required fields');
                return;
            }
            
            // Create post
            const newPost = State.db.posts.create({
                title,
                content,
                category,
                tags: tags.split(',').map(tag => tag.trim()).filter(tag => tag),
                isPublished,
                author: { id: State.user.id, name: State.user.name }
            });
            
            // Redirect to the new post
            Router.navigate(`/posts/${newPost.id}`);
        }
        
        function handleAddComment(event, postId) {
            event.preventDefault();
            
            const content = document.getElementById('comment-content').value;
            
            if (!content.trim()) {
                alert('Please enter a comment');
                return;
            }
            
            // Add comment
            State.db.posts.addComment(postId, {
                user: { name: State.user.name },
                content: content
            });
            
            // Clear the form and refresh the page
            document.getElementById('comment-content').value = '';
            Router.navigate(`/posts/${postId}`);
        }
        
        function showError(elementId, message) {
            const errorElement = document.getElementById(elementId);
            const errorText = document.getElementById(`${elementId}-text`);
            
            errorText.textContent = message;
            errorElement.classList.remove('hidden');
            
            // Hide error after 5 seconds
            setTimeout(() => {
                errorElement.classList.add('hidden');
            }, 5000);
        }

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            // Initialize state
            State.init();
            
            // Add routes
            Router.addRoute('/', function() {
                renderApp(Components.Home());
            });
            
            Router.addRoute('/posts', function() {
                renderApp(Components.Posts());
            });
            
            Router.addRoute('/posts/:id', function() {
                renderApp(Components.Post());
            });
            
            Router.addRoute('/create-post', function() {
                renderApp(Components.CreatePost());
            });
            
            Router.addRoute('/login', function() {
                renderApp(Components.Login());
            });
            
            Router.addRoute('/register', function() {
                renderApp(Components.Register());
            });
            
            Router.addRoute('/profile', function() {
                renderApp(Components.Profile());
            });
            
            // Initialize router
            Router.init();
            
            // Add mobile menu toggle
            document.addEventListener('click', function(e) {
                if (e.target.id === 'mobile-menu-button' || e.target.closest('#mobile-menu-button')) {
                    const mobileMenu = document.getElementById('mobile-menu');
                    mobileMenu.classList.toggle('hidden');
                }
            });
        });
        
        // Render the application
        function renderApp(content) {
            document.getElementById('app').innerHTML = `
                ${Components.Header()}
                <main class="flex-grow">
                    ${content}
                </main>
                ${Components.Footer()}
            `;
        }
    </script>
</body>
</html>
