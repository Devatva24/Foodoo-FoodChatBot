# 🍔 Foodoo – Food Delivery Chatbot  

Foodoo is a **Food Delivery Chatbot** built using **Dialogflow**, **FastAPI**, and a simple **SQL database**. It allows users to browse the menu, place orders, and track their order status through an interactive chatbot interface.  

The project also includes a **frontend website** with chatbot integration and backend APIs connected to a database.  

---

## 📂 Project Structure  

```
Foodoo-FoodChatBot-master/
│── README.md               # Project documentation
│── requirements.txt        # Python dependencies
│── main.py                 # FastAPI backend server
│── db_helper.py            # Database helper functions
│── generic_helper.py       # Generic helper functions
│── ngrok.exe               # Local tunneling tool
│
├── db/
│   └── pandeyji_eatery.sql  # Database schema & sample data
│
├── dialogflow_assets/
│   └── training_phrases.txt # Dialogflow intents/training phrases
│
├── frontend/
│   ├── home.html            # Website with chatbot integration
│   ├── styles.css           # Stylesheet
│   ├── banner.jpg
│   ├── menu1.jpg
│   ├── menu2.jpg
│   └── menu3.jpg
│
└── .idea/                   # IDE settings (ignore in deployment)
```

---

## 🚀 Features  

- 💬 **Dialogflow Chatbot** – Handles conversations with users.  
- 🗄 **SQL Database** – Stores menu items, orders, and order status.  
- 🔌 **FastAPI Backend** – Webhook for Dialogflow to fetch and update order details.  
- 🌍 **Ngrok Integration** – Expose local server for Dialogflow webhook.  
- 🎨 **Frontend Website** – Includes chatbot widget, menu, and contact page.  

---

## ⚙️ Installation & Setup  

### 1️⃣ Clone the Repository  
```bash
git clone https://github.com/your-username/Foodoo-FoodChatBot.git
cd Foodoo-FoodChatBot-master
```

### 2️⃣ Create Virtual Environment & Install Dependencies  
```bash
python -m venv venv
source venv/bin/activate   # On Linux/Mac
venv\Scripts\activate      # On Windows

pip install -r requirements.txt
```

### 3️⃣ Setup Database  
- Import the SQL schema:  
```bash
sqlite3 foodoo.db < db/pandeyji_eatery.sql
```
*(or use MySQL/Postgres if modifying `db_helper.py`)*  

### 4️⃣ Run Backend Server  
```bash
uvicorn main:app --reload --port 9000
```

### 5️⃣ Expose with Ngrok  
```bash
ngrok http 9000
```
Copy the **public ngrok URL** and set it as the **Webhook URL** in **Dialogflow console**.  

---

## 🎯 Dialogflow Integration  

- Create a new **Dialogflow Agent**.  
- Import intents and training phrases from `dialogflow_assets/`.  
- Configure the **Webhook URL** (`https://<ngrok-id>.ngrok.io/webhook`).  
- Enable webhook for order-related intents (e.g., *order.add*, *order.complete*, *order.track*).  

---

## 🌐 Frontend Integration  

- Open `frontend/home.html` in a browser.  
- The chatbot iframe is already embedded.  
- You can modify branding in `styles.css`.  

---

## 🛠 Tech Stack  

- **Backend**: FastAPI (Python)  
- **Database**: SQLite/MySQL (SQL schema provided)  
- **NLP**: Dialogflow CX/ES  
- **Frontend**: HTML, CSS  
- **Tools**: Ngrok, REST APIs  

---

## 📸 Screenshots  

**Home Page with Chatbot Widget**  
*(Add screenshots here)*  

---

## 📜 License  

This project is licensed under the **MIT License**.  
Feel free to use, modify, and distribute with attribution.  
