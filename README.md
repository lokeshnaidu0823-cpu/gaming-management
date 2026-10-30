# gaming-management
from flask import Flask, render_template, request, redirect

app = Flask(__name__)

games = [
    {"id": 1, "name": "GTA V", "price": 500},
    {"id": 2, "name": "Minecraft", "price": 300},
    {"id": 3, "name": "PUBG", "price": 200}
]

@app.route('/')
def home():
    return render_template('index.html', games=games)

@app.route('/games')
def show_games():
    return render_template('games.html', games=games)

@app.route('/add_game', methods=['POST'])
def add_game():
    name = request.form['name']
    price = request.form['price']

    games.append({
        "id": len(games) + 1,
        "name": name,
        "price": price
    })

    return redirect('/games')

if __name__ == '__main__':
    app.run(debug=True)
