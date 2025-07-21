# Adventure Works E-Commerce Platform

A modern, minimalist e-commerce web application built with C# ASP.NET Core backend API and Angular frontend, showcasing products from the Adventure Works database.

## 🎯 Project Overview

Adventure Works E-Commerce is a full-stack web application that transforms the classic Adventure Works product catalog into a beautiful, intuitive online shopping experience. The platform emphasizes clean design, high performance, and scalable architecture.

### ✨ Key Features

- 🛍️ **Product Catalog**: Browse and search Adventure Works products
- 🛒 **Shopping Cart**: Add, modify, and manage cart items  
- 💳 **Secure Checkout**: Complete purchase flow with payment processing
- 👤 **User Management**: Registration, authentication, and profile management
- 📱 **Responsive Design**: Mobile-first, beautiful UI across all devices
- ⚡ **Performance**: Fast loading times with caching and optimization

## 🏗️ Architecture

The application follows **Clean Architecture** principles with clear separation of concerns:

### Backend (C# ASP.NET Core 8.0)
```
src/
├── AdventureWorks.Domain/           # Domain entities and business rules
├── AdventureWorks.Application/      # Use cases and application logic
├── AdventureWorks.Infrastructure/   # Data access and external services  
└── AdventureWorks.API/             # Web API controllers and middleware

tests/
├── AdventureWorks.UnitTests/        # Unit tests
└── AdventureWorks.IntegrationTests/ # Integration tests
```

### Frontend (Angular 17+)
```
adventure-works-ui/
├── src/app/
│   ├── core/                        # Singleton services and guards
│   ├── shared/                      # Reusable components  
│   ├── features/                    # Feature modules (products, cart, etc.)
│   ├── state/                       # NgRx state management
│   └── models/                      # TypeScript interfaces
├── src/assets/                      # Static assets
└── src/styles/                      # Global SCSS styles
```

## 🛠️ Technology Stack

### Backend
- **Framework**: ASP.NET Core 8.0 Web API
- **Database**: SQL Server with Adventure Works schema
- **ORM**: Entity Framework Core
- **Architecture**: Clean Architecture + CQRS
- **Authentication**: JWT with refresh tokens
- **Caching**: Redis
- **Documentation**: Swagger/OpenAPI
- **Logging**: Serilog

### Frontend  
- **Framework**: Angular 17+ with standalone components
- **State Management**: NgRx Store
- **UI Library**: Angular Material with custom theming
- **Styling**: SCSS with CSS Grid/Flexbox
- **Testing**: Jasmine/Karma (unit), Cypress (E2E)
- **Build**: Angular CLI with Vite

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **Cloud**: Azure/AWS ready
- **CI/CD**: GitHub Actions
- **Monitoring**: Application Insights

## 🚀 Quick Start

### Prerequisites
- .NET 8.0 SDK
- Node.js 20.x LTS  
- Angular CLI 17+
- SQL Server 2022
- Docker Desktop

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd AdvWebApp
   ```

2. **Backend setup**
   ```bash
   cd src
   dotnet restore
   dotnet run --project AdventureWorks.API
   ```

3. **Frontend setup**  
   ```bash
   cd adventure-works-ui
   npm install
   ng serve
   ```

4. **Access the application**
   - Frontend: http://localhost:4200
   - Backend API: https://localhost:5001/swagger

## 📋 Development Status

### ✅ Completed
- [x] Project initialization and Git setup
- [x] Clean Architecture folder structure  
- [x] Project documentation and planning

### 🔄 In Progress
- [ ] ASP.NET Core Web API setup
- [ ] Angular application setup
- [ ] Database configuration

### 📅 Upcoming  
- [ ] Authentication system
- [ ] Product catalog implementation
- [ ] Shopping cart functionality
- [ ] Checkout and payment processing

## 🎨 Design Principles

- **Minimalist**: Clean, uncluttered interface focusing on products
- **Performance**: Sub-3-second page loads globally
- **Accessibility**: WCAG 2.1 AA compliance
- **Mobile-First**: Responsive design for all screen sizes  
- **User-Centric**: Intuitive navigation and seamless user experience

## 📖 Documentation

- **[Planning Guide](planning.md)**: Vision, architecture, and technical requirements
- **[Claude Guide](claude.md)**: AI assistant guide for development sessions  
- **[Task Breakdown](tasks.md)**: Detailed development milestones and tasks
- **[Backend Guide](src/README.md)**: Clean Architecture implementation details
- **[Frontend Guide](adventure-works-ui/README.md)**: Angular feature structure
- **[Testing Guide](tests/README.md)**: Unit and integration testing approach

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)  
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For questions and support:
- Create an issue in the repository
- Review the documentation in the `/docs` directory  
- Check the troubleshooting guide in `claude.md`

---

**Adventure Works E-Commerce Platform** - Transforming product catalogs into beautiful shopping experiences.
