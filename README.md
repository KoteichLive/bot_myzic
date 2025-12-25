# 🤖 Bot Muzik - Advanced AIogram Telegram Bot

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![aiogram](https://img.shields.io/badge/aiogram-3.x-green.svg)](https://github.com/aiogram/aiogram)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A comprehensive Telegram bot built with aiogram 3.x for music and content management, featuring admin approval system, categories, promo codes, cases, and advertising marketplace.

## 📋 Table of Contents

- [Features](#-features)
- [Architecture](#-architecture)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Database Schema](#-database-schema)
- [Development](#-development)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

## 🎵 Features

### 👤 User Features
- **Content Submission**: Submit music files and text posts for admin approval
- **Music Library**: Browse approved music organized by categories and tags
- **Promo Codes**: Create and activate promotional codes with rewards
- **Cases System**: Participate in free/paid cases for random rewards
- **Advertising**: Place advertisements in channels with budget management
- **Balance Management**: View balance, transaction history, transfers
- **Statistics**: Personal usage statistics and earnings tracking

### 👨‍💼 Administrator Features
- **Content Moderation**: Approve/reject music, posts, and advertisements
- **Category Management**: Create and manage music categories and tags
- **User Management**: View user statistics, manage balances, ban/unban users
- **Promo Management**: Create system-wide promo codes
- **Advertising Oversight**: Review and approve ad campaigns
- **Analytics Dashboard**: System-wide statistics and insights

### 📺 Channel Features
- **Automated Publishing**: Scheduled posting of approved content
- **Reward System**: Automatic rewards for adding bot to channels
- **Advertising Integration**: Monetization through approved advertisements

## 🏗️ Architecture

```
bot_muzik/
├── 📁 main.py                 # Application entry point
├── 📁 config.py               # Configuration settings
├── 📁 requirements.txt        # Python dependencies
├── 📁 database/
│   ├── 📄 models.py           # SQLAlchemy ORM models
│   └── 📄 connection.py       # Database connection management
├── 📁 handlers/
│   └── 📄 user.py             # User command handlers
├── 📁 keyboards/
│   ├── 📄 user_kb.py          # User interface keyboards
│   ├── 📄 admin_kb.py         # Admin interface keyboards
│   └── 📄 inline_kb.py        # Inline keyboards
├── 📁 routers/
│   └── 📄 user_router.py      # User command routing
├── 📁 middlewares/
│   ├── 📄 auth.py             # Authentication & user management
│   └── 📄 logging.py          # Request logging
├── 📁 utils/
│   ├── 📄 helpers.py          # Utility functions
│   ├── 📄 scheduler.py        # Background task scheduler
│   └── 📄 validators.py       # Input validation
├── 📁 api/
│   ├── 📄 app.py              # FastAPI application
│   ├── 📄 routes.py           # API endpoints
│   └── 📄 auth.py             # API authentication
├── 📁 states/
│   ├── 📄 user_states.py      # FSM states for users
│   └── 📄 admin_states.py     # FSM states for admins
└── 📄 README.md               # Documentation
```

### 🛠️ Technical Stack

- **Framework**: aiogram 3.x (Telegram Bot API)
- **Web Framework**: FastAPI (REST API)
- **Database**: SQLAlchemy with async support (SQLite/PostgreSQL)
- **State Management**: aiogram FSM with Redis/Memory storage
- **Task Scheduling**: APScheduler
- **Validation**: Pydantic
- **Logging**: Loguru

## 🚀 Installation

### Prerequisites
- Python 3.8 or higher
- Git
- Virtual environment (recommended)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/bot-muzik.git
   cd bot-muzik
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   # or
   venv\Scripts\activate     # Windows
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure the bot** (see Configuration section below)

5. **Run the bot**
   ```bash
   python main.py
   ```

## ⚙️ Configuration

Create a `config.py` file in the root directory:

```python
# Telegram Bot Configuration
BOT_TOKEN = "1234567890:ABCdefGHIjklMNOpqrsTUVwxyz123456789"  # Get from @BotFather
ADMIN_IDS = [123456789, 987654321]  # Telegram user IDs of administrators

# Database Configuration
DATABASE_URL = "sqlite+aiosqlite:///bot.db"  # SQLite (recommended for development)
# DATABASE_URL = "postgresql+asyncpg://user:password@localhost:5432/bot_db"  # PostgreSQL

# State Storage (choose one)
REDIS_URL = "redis://localhost:6379"  # Redis for production
# Use MemoryStorage for development (automatically configured)

# API Server Configuration
API_HOST = "0.0.0.0"
API_PORT = 8000
API_SECRET_KEY = "your-super-secret-key-change-this-in-production"

# Logging Configuration
LOG_LEVEL = "INFO"
LOG_FILE = "bot.log"

# Business Logic Settings
DEFAULT_BALANCE = 0.0
FREE_CASE_REWARD = 10.0
POST_SUBMIT_REWARD = 5.0
MESSAGE_REWARD = 1.0
VOICE_REWARD = 2.0
ADMIN_FEE_PERCENT = 10.0
CHANNEL_ADD_REWARD = 50.0

# Promo Code Settings
PROMO_CODE_LENGTH = 8
PROMO_ACTIVATION_REWARD = 0.0

# Case Settings
CASE_PARTICIPATION_LIMIT = 1

# Advertisement Settings
MIN_AD_BUDGET = 10.0
MAX_AD_BUDGET = 1000.0

# File Upload Limits
MAX_MUSIC_FILE_SIZE = 50 * 1024 * 1024  # 50 MB
ALLOWED_MUSIC_FORMATS = ['mp3', 'wav', 'flac', 'aac', 'ogg']
MAX_PHOTO_SIZE = 10 * 1024 * 1024  # 10 MB

# Scheduler Settings
SCHEDULER_TIMEZONE = "Europe/Moscow"

# Webhook Settings (optional, for production)
WEBHOOK_URL = ""  # Leave empty for polling mode
WEBHOOK_PATH = "/webhook"
WEBHOOK_SECRET = "webhook-secret-change-this"

# Payment Integration (if needed)
PAYMENT_TOKEN = ""

# External API Settings
EXTERNAL_API_TIMEOUT = 30

# Database Connection Pool
DB_POOL_SIZE = 10
DB_MAX_OVERFLOW = 20

# Redis Pool (if using Redis)
REDIS_POOL_SIZE = 10

# Rate Limiting
RATE_LIMIT_REQUESTS = 30  # requests per window
RATE_LIMIT_WINDOW = 60    # seconds

# Caching
CACHE_TTL = 300  # 5 minutes
```

### Environment Variables (Alternative)

You can also use environment variables for sensitive configuration:

```bash
export BOT_TOKEN="your_bot_token"
export DATABASE_URL="sqlite+aiosqlite:///bot.db"
export API_SECRET_KEY="your-secret-key"
python main.py
```

## 📖 Usage

### For Users

1. **Start the bot**: Send `/start` command to @your_bot_username
2. **Navigate menus**: Use inline keyboards to access different sections
3. **Submit content**: Upload music or write posts for admin approval
4. **Earn rewards**: Participate in activities and invite friends
5. **Manage balance**: View transactions and transfer funds

### For Administrators

1. **Access admin panel**: Bot automatically detects admin users
2. **Moderate content**: Review submissions in approval queues
3. **Manage categories**: Create music categories and tags
4. **User management**: View statistics and manage user accounts
5. **System monitoring**: Check bot performance and usage statistics

### Available Commands

| Command | Description |
|---------|-------------|
| `/start` | Initialize bot and show welcome message |
| `/help` | Show help information |
| `/menu` | Display main menu |

### Keyboard Navigation

The bot uses inline keyboards for intuitive navigation:
- **🎵 Music**: Browse and listen to approved music
- **📝 Submit Post**: Propose content for publication
- **🎫 Promo Codes**: Create and manage promotional codes
- **🎰 Cases**: Participate in reward cases
- **📢 Advertising**: Place advertisements
- **💰 Balance**: Manage account balance
- **📊 Statistics**: View personal statistics
- **ℹ️ Help**: Access help and rules

## 🌐 API Documentation

The bot includes a REST API for external integrations.

### Authentication

API uses Bearer token authentication:
```
Authorization: Bearer <your-api-token>
```

### Endpoints

#### 🎫 Promo Codes
```http
GET /promo/{code}
POST /promo/{code}/activate
```

#### 👤 Users
```http
GET /users/{user_id}/balance
POST /users/{user_id}/reward
```

#### 📺 Channels
```http
GET /channels
POST /channels/{channel_id}/post
```

#### 📊 Health Check
```http
GET /health
```

### API Usage Examples

**Get Promo Code Info:**
```bash
curl -H "Authorization: Bearer your-token" \
     http://localhost:8000/promo/ABC123
```

**Activate Promo Code:**
```bash
curl -X POST \
     -H "Authorization: Bearer your-token" \
     -H "Content-Type: application/json" \
     -d '{}' \
     http://localhost:8000/promo/ABC123/activate
```

## 🗄️ Database Schema

### Core Tables

#### Users
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    telegram_id BIGINT UNIQUE NOT NULL,
    username VARCHAR(255),
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    language_code VARCHAR(10),
    balance FLOAT DEFAULT 0.0,
    is_admin BOOLEAN DEFAULT FALSE,
    is_banned BOOLEAN DEFAULT FALSE,
    last_active TIMESTAMP,
    messages_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Music
```sql
CREATE TABLE music (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    file_id VARCHAR(255) NOT NULL,
    title VARCHAR(255) NOT NULL,
    artist VARCHAR(255) NOT NULL,
    category_id INTEGER REFERENCES categories(id),
    tags JSON,
    approved BOOLEAN DEFAULT FALSE,
    submitted_by INTEGER REFERENCES users(id),
    approved_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Categories & Tags
```sql
CREATE TABLE categories (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name VARCHAR(255) UNIQUE NOT NULL,
    description TEXT NOT NULL,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE tags (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name VARCHAR(255) UNIQUE NOT NULL,
    category_id INTEGER REFERENCES categories(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Posts & Publishing
```sql
CREATE TABLE posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    text TEXT NOT NULL,
    scheduled_at TIMESTAMP,
    approved BOOLEAN DEFAULT FALSE,
    submitted_by INTEGER REFERENCES users(id),
    approved_by INTEGER REFERENCES users(id),
    published_in JSON,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Promo Codes
```sql
CREATE TABLE promo_codes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    code VARCHAR(255) UNIQUE NOT NULL,
    amount FLOAT NOT NULL,
    comment TEXT NOT NULL,
    created_by INTEGER REFERENCES users(id),
    activated_by INTEGER REFERENCES users(id),
    activated_at TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Cases & Rewards
```sql
CREATE TABLE cases (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    price FLOAT DEFAULT 0.0,
    rewards JSON,
    is_free BOOLEAN DEFAULT FALSE,
    created_by INTEGER REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE case_participations (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER REFERENCES users(id),
    case_id INTEGER REFERENCES cases(id),
    reward_amount FLOAT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Advertising
```sql
CREATE TABLE advertisements (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    text TEXT NOT NULL,
    photo_file_id VARCHAR(255),
    channels JSON,
    price_per_post FLOAT NOT NULL,
    total_budget FLOAT NOT NULL,
    approved BOOLEAN DEFAULT FALSE,
    submitted_by INTEGER REFERENCES users(id),
    approved_by INTEGER REFERENCES users(id),
    admin_comment TEXT DEFAULT '',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Channels
```sql
CREATE TABLE channels (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    telegram_id BIGINT UNIQUE NOT NULL,
    title VARCHAR(255) NOT NULL,
    owner_id INTEGER REFERENCES users(id),
    reward_per_post FLOAT DEFAULT 0.0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 💻 Development

### Development Setup

1. **Install development dependencies**
   ```bash
   pip install -r requirements-dev.txt  # if available
   ```

2. **Enable debug logging**
   ```python
   LOG_LEVEL = "DEBUG"
   ```

3. **Run with auto-reload**
   ```bash
   python -m uvicorn api.app:app --reload --host 0.0.0.0 --port 8000
   ```

### Code Structure Guidelines

- **Handlers**: Keep business logic separate from message handling
- **Models**: Use SQLAlchemy best practices with proper relationships
- **Middleware**: Implement cross-cutting concerns (auth, logging, rate limiting)
- **Keyboards**: Centralize UI components for consistency
- **Utils**: Pure functions for reusable logic

### Adding New Features

1. **Plan the feature**: Define requirements and user stories
2. **Database changes**: Create migrations for schema updates
3. **Implement handlers**: Add command/message handlers
4. **Update keyboards**: Create or modify UI components
5. **Add middleware**: Implement necessary cross-cutting concerns
6. **Write tests**: Ensure functionality works correctly
7. **Update documentation**: Reflect changes in README and API docs

## 🧪 Testing

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=bot_muzik --cov-report=html

# Run specific test file
pytest tests/test_handlers.py

# Run tests in verbose mode
pytest -v
```

### Test Structure

```
tests/
├── conftest.py           # Test configuration and fixtures
├── test_handlers/        # Handler tests
├── test_models/          # Model tests
├── test_api/             # API endpoint tests
├── test_middlewares/     # Middleware tests
└── test_utils/           # Utility function tests
```

### Writing Tests

```python
import pytest
from aiogram.types import Message

def test_start_command(user_message):
    # Test /start command handler
    response = await handle_start_command(user_message)
    assert "welcome" in response.text.lower()
```

## 🚀 Deployment

### Production Checklist

- [ ] Set `LOG_LEVEL = "WARNING"` or `"ERROR"`
- [ ] Use PostgreSQL instead of SQLite
- [ ] Configure Redis for state storage
- [ ] Set strong `API_SECRET_KEY`
- [ ] Enable webhooks instead of polling
- [ ] Configure SSL/TLS certificates
- [ ] Set up monitoring and alerts
- [ ] Configure backup procedures
- [ ] Set up log rotation

### Docker Deployment

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 8000

CMD ["python", "main.py"]
```

```bash
# Build and run
docker build -t bot-muzik .
docker run -d -p 8000:8000 --env-file .env bot-muzik
```

### Systemd Service

Create `/etc/systemd/system/bot-muzik.service`:

```ini
[Unit]
Description=Bot Muzik Telegram Bot
After=network.target

[Service]
Type=simple
User=botuser
WorkingDirectory=/opt/bot-muzik
ExecStart=/opt/bot-muzik/venv/bin/python main.py
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable bot-muzik
sudo systemctl start bot-muzik
sudo systemctl status bot-muzik
```

### Webhook Configuration

For production, configure webhooks instead of polling:

```python
WEBHOOK_URL = "https://your-domain.com"
WEBHOOK_PATH = "/webhook"
WEBHOOK_SECRET = "your-webhook-secret"
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make your changes** and add tests
4. **Run tests**: `pytest`
5. **Commit changes**: `git commit -m 'Add amazing feature'`
6. **Push to branch**: `git push origin feature/amazing-feature`
7. **Open a Pull Request**

### Contribution Guidelines

- Follow PEP 8 style guidelines
- Write comprehensive tests for new features
- Update documentation for API changes
- Use type hints for function parameters
- Keep commit messages descriptive and concise
- Ensure all tests pass before submitting PR

### Code Review Process

- All PRs require review from at least one maintainer
- CI/CD pipeline must pass all checks
- Code coverage should not decrease
- Documentation must be updated for user-facing changes

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/your-username/bot-muzik/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-username/bot-muzik/discussions)
- **Documentation**: [Wiki](https://github.com/your-username/bot-muzik/wiki)

## 🙏 Acknowledgments

- [aiogram](https://github.com/aiogram/aiogram) - Modern Telegram Bot Framework
- [FastAPI](https://fastapi.tiangolo.com/) - Modern Python web framework
- [SQLAlchemy](https://www.sqlalchemy.org/) - Python SQL toolkit
- [Loguru](https://github.com/Delgan/loguru) - Python logging made simple

---

**Made with ❤️ for the Telegram community**
