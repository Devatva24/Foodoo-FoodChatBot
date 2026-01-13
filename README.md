# 🍔 Foodoo - AI-Powered Food Delivery Chatbot

An intelligent conversational food ordering system built with Google Dialogflow, FastAPI, and MySQL. Foodoo enables customers to browse menus, place orders, and track deliveries through natural language conversations, providing a seamless ordering experience.

[![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat&logo=python)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.68+-green?style=flat&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Dialogflow](https://img.shields.io/badge/Dialogflow-CX-orange?style=flat&logo=google)](https://cloud.google.com/dialogflow)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## ✨ Features

- 🤖 **Natural Language Processing**: Powered by Google Dialogflow for understanding user intent
- 🍕 **Menu Browsing**: Interactive menu exploration through conversation
- 🛒 **Order Management**: Add items, modify quantities, and complete orders
- 📦 **Order Tracking**: Real-time order status updates
- 💾 **Database Integration**: MySQL backend for persistent storage
- 🌐 **Web Interface**: Beautiful frontend with embedded chatbot
- ⚡ **FastAPI Backend**: High-performance RESTful API
- 🔄 **Session Management**: Context-aware conversations
- 📱 **Responsive Design**: Works seamlessly across devices

## 🎯 Demo

Try Foodoo in action:
- Browse the menu: *"Show me the menu"*
- Place an order: *"I want 2 pizzas and 1 burger"*
- Track order: *"What's my order status?"*
- Modify order: *"Add 1 more pizza"*

## 🏗️ Architecture

```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐
│   User      │─────▶│  Dialogflow  │─────▶│   FastAPI   │
│  (Frontend) │      │  (NLP Agent) │      │  (Backend)  │
└─────────────┘      └──────────────┘      └─────────────┘
                            │                      │
                            │                      ▼
                            │               ┌─────────────┐
                            └──────────────▶│   MySQL DB  │
                                            │  (Storage)  │
                                            └─────────────┘
```

### Conversation Flow

```
User → "I want 2 pizzas" 
    ↓
Dialogflow extracts: {item: "pizza", quantity: 2}
    ↓
Webhook → FastAPI → Database
    ↓
Response ← "Added 2 pizzas to your order!"
```

## 📋 Prerequisites

- Python 3.8 or higher
- MySQL Server (or SQLite for testing)
- Google Cloud account (for Dialogflow)
- Ngrok account (for local development)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Devatva24/Foodoo-FoodChatBot.git
cd Foodoo-FoodChatBot
```

### 2. Create Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

**Dependencies include:**
- FastAPI - Web framework
- uvicorn - ASGI server
- mysql-connector-python - Database connector
- pydantic - Data validation
- python-dotenv - Environment variables

### 4. Setup Database

#### Using MySQL:

```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE pandeyji_eatery;

# Import schema
mysql -u root -p pandeyji_eatery < db/pandeyji_eatery.sql
```

#### Using SQLite (for testing):

```bash
sqlite3 foodoo.db < db/pandeyji_eatery.sql
```

### 5. Configure Environment Variables

Create a `.env` file in the root directory:

```env
# Database Configuration
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=pandeyji_eatery

# Server Configuration
PORT=9000
HOST=0.0.0.0

# Dialogflow Configuration
PROJECT_ID=your-dialogflow-project-id
```

### 6. Run the Backend Server

```bash
uvicorn main:app --reload --port 9000
```

The API will be available at `http://localhost:9000`

### 7. Setup Ngrok (for Dialogflow Webhook)

```bash
# Start ngrok
ngrok http 9000
```

Copy the HTTPS URL (e.g., `https://abc123.ngrok.io`)

## 🤖 Dialogflow Configuration

### 1. Create Dialogflow Agent

1. Go to [Dialogflow Console](https://dialogflow.cloud.google.com/)
2. Create a new agent named "Foodoo"
3. Set the default language and timezone

### 2. Import Intents

Import the training phrases from `dialogflow_assets/`:

**Key Intents:**
- `new.order` - Start a new order
- `order.add` - Add items to order
- `order.remove` - Remove items from order
- `order.complete` - Finalize the order
- `track.order` - Check order status

### 3. Configure Webhook

1. Go to **Fulfillment** section
2. Enable **Webhook**
3. Enter your ngrok URL: `https://your-ngrok-id.ngrok.io/webhook`
4. Save

### 4. Enable Webhook for Intents

For each intent:
1. Scroll to **Fulfillment** section
2. Enable **"Enable webhook call for this intent"**
3. Save

### 5. Training Phrases Examples

**order.add intent:**
```
- I want 2 pizzas
- Add 1 burger to my order
- Can I get 3 pasta dishes
- 2 margherita pizzas please
- Add one large coke
```

**track.order intent:**
```
- What's my order status?
- Track my order
- Where is my order?
- Order status please
```

## 🌐 Frontend Setup

### 1. Update Chatbot Integration

Edit `frontend/home.html` and update the Dialogflow integration code:

```html
<script src="https://www.gstatic.com/dialogflow-console/fast/messenger/bootstrap.js?v=1"></script>
<df-messenger
  chat-title="Foodoo"
  agent-id="YOUR-AGENT-ID"
  language-code="en">
</df-messenger>
```

### 2. Serve the Frontend

```bash
# Using Python's built-in server
cd frontend
python -m http.server 8080
```

Visit `http://localhost:8080/home.html`

## 📁 Project Structure

```
Foodoo-FoodChatBot/
├── frontend/
│   ├── home.html           # Main website with chatbot
│   ├── styles.css          # Styling
│   ├── banner.jpg          # Header image
│   ├── menu1.jpg           # Menu images
│   ├── menu2.jpg
│   └── menu3.jpg
├── db/
│   └── pandeyji_eatery.sql # Database schema & data
├── dialogflow_assets/
│   └── training_phrases.txt # Sample intents
├── main.py                 # FastAPI application
├── db_helper.py            # Database operations
├── generic_helper.py       # Utility functions
├── requirements.txt        # Python dependencies
├── ngrok.exe              # Tunneling tool (Windows)
└── README.md              # Documentation
```

## 🔧 API Endpoints

### Webhook Endpoint

```http
POST /webhook
Content-Type: application/json

{
  "queryResult": {
    "intent": {
      "displayName": "order.add"
    },
    "parameters": {
      "food-item": ["pizza"],
      "number": [2]
    }
  },
  "session": "projects/.../sessions/..."
}
```

**Response:**
```json
{
  "fulfillmentText": "Added 2 pizzas to your order!"
}
```

## 💡 Usage Examples

### Starting an Order

```
User: Hi, I want to place an order
Bot: Great! What would you like to order?
User: 2 pizzas and 1 burger
Bot: Added 2 pizzas and 1 burger to your order. Anything else?
User: That's all
Bot: Your order total is $25.99. Confirm order?
User: Yes
Bot: Order confirmed! Your order ID is #1234
```

### Tracking an Order

```
User: Track my order 1234
Bot: Your order #1234 is being prepared. Estimated delivery: 30 minutes
```

### Modifying an Order

```
User: Add 1 more pizza
Bot: Added 1 pizza. Your order now has 3 pizzas and 1 burger
User: Remove the burger
Bot: Removed burger from your order
```

## 🗄️ Database Schema

### Tables

**food_items**
```sql
CREATE TABLE food_items (
    item_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255),
    price DECIMAL(10,2)
);
```

**orders**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    total_price DECIMAL(10,2),
    status VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**order_items**
```sql
CREATE TABLE order_items (
    item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    food_item_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (food_item_id) REFERENCES food_items(item_id)
);
```

**order_tracking**
```sql
CREATE TABLE order_tracking (
    order_id INT PRIMARY KEY,
    status VARCHAR(50),
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);
```

## 🔒 Security Best Practices

1. **Environment Variables**: Never commit `.env` files
2. **API Keys**: Use environment variables for sensitive data
3. **Database**: Use parameterized queries (already implemented)
4. **HTTPS**: Always use HTTPS for webhooks in production
5. **Input Validation**: Validate all user inputs (implemented with Pydantic)

## 🚀 Deployment

### Deploy to Heroku

```bash
# Install Heroku CLI
heroku login

# Create app
heroku create foodoo-chatbot

# Add database
heroku addons:create cleardb:ignite

# Deploy
git push heroku master

# Update Dialogflow webhook URL
# https://foodoo-chatbot.herokuapp.com/webhook
```

### Deploy to AWS

1. Set up EC2 instance
2. Install dependencies
3. Configure MySQL RDS
4. Use Nginx as reverse proxy
5. Set up SSL with Let's Encrypt
6. Update Dialogflow webhook

### Deploy to Google Cloud

```bash
# Deploy to Cloud Run
gcloud run deploy foodoo \
  --source . \
  --region us-central1 \
  --allow-unauthenticated
```

## 🧪 Testing

### Test the API

```bash
# Health check
curl http://localhost:9000/

# Test webhook
curl -X POST http://localhost:9000/webhook \
  -H "Content-Type: application/json" \
  -d @test_payload.json
```

### Test Dialogflow

1. Use **Try it now** panel in Dialogflow Console
2. Test various intents and scenarios
3. Check webhook calls in FastAPI logs

## 🐛 Troubleshooting

### Issue: Webhook not responding

**Solution:**
- Check if FastAPI server is running
- Verify ngrok is active and URL is updated in Dialogflow
- Check FastAPI logs for errors

### Issue: Database connection error

**Solution:**
- Verify MySQL is running
- Check credentials in `.env` file
- Test connection: `mysql -u root -p`

### Issue: Dialogflow not recognizing intent

**Solution:**
- Add more training phrases
- Retrain the agent
- Check entity extraction in parameters

### Issue: Session context lost

**Solution:**
- Enable Dialogflow session management
- Check session parameters in webhook payload

## 🎨 Customization

### Adding New Menu Items

```python
# In db_helper.py
def add_menu_item(name, price):
    cursor.execute(
        "INSERT INTO food_items (name, price) VALUES (%s, %s)",
        (name, price)
    )
    db.commit()
```

### Custom Intents

1. Create new intent in Dialogflow
2. Add webhook fulfillment
3. Implement handler in `main.py`:

```python
@app.post("/webhook")
async def handle_webhook(request: Request):
    intent = request["queryResult"]["intent"]["displayName"]
    
    if intent == "custom.intent":
        return custom_intent_handler(request)
```

### Styling Frontend

Edit `frontend/styles.css`:

```css
/* Custom theme colors */
:root {
    --primary-color: #ff6b6b;
    --secondary-color: #4ecdc4;
    --background-color: #f7f7f7;
}
```

## 📊 Analytics & Monitoring

Add logging for tracking:

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.post("/webhook")
async def handle_webhook(request: Request):
    logger.info(f"Received intent: {intent_name}")
    # Process request
```

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Areas for Contribution

- [ ] Payment gateway integration
- [ ] Multi-restaurant support
- [ ] Voice ordering capability
- [ ] Order history dashboard
- [ ] Rating and review system
- [ ] Delivery tracking map
- [ ] Mobile app integration

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Google Dialogflow](https://cloud.google.com/dialogflow) - NLP platform
- [FastAPI](https://fastapi.tiangolo.com/) - Web framework
- [Ngrok](https://ngrok.com/) - Secure tunneling
- [MySQL](https://www.mysql.com/) - Database system

## 👤 Author

**Devatva Rachit**

- GitHub: [@Devatva24](https://github.com/Devatva24)
- Project: [Foodoo](https://github.com/Devatva24/Foodoo-FoodChatBot)

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!

## 🔮 Future Enhancements

- [ ] Multi-language support
- [ ] Voice interface integration
- [ ] Payment processing (Stripe/PayPal)
- [ ] Restaurant dashboard
- [ ] Customer loyalty program
- [ ] AI-powered recommendations
- [ ] Real-time delivery tracking
- [ ] Push notifications
- [ ] Social media integration

---

**Built with 💙 and 🍕 by Devatva Rachit**
