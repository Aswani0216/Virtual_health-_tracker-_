from flask import Flask, request, jsonify
from datetime import datetime

app = Flask(__name__)


health_data = []

@app.route('/log_data', methods=['POST'])
def log_data():
    data = request.get_json()


    if not data or not data.get("user_id") or not data.get("metric") or not data.get("value"):
        return jsonify({"error": "Missing required fields"}), 400

    health_data.append({
        "timestamp": datetime.now().isoformat(),
        "user_id": data["user_id"],
        "metric": data["metric"],
        "value": data["value"]
    })
    return jsonify({"message": "Data logged successfully"}), 201

@app.route('/get_data/<user_id>', methods=['GET'])
def get_data(user_id):
    user_records = [item for item in health_data if item["user_id"] == user_id]
    return jsonify(user_records), 200

if __name__ == '__main__':

    app.run(debug=True, host='0.0.0.0', port=5000)
