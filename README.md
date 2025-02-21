# bajajfinserv
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/bfhl', methods=['POST'])
def process_data():
    try:
        if not request.is_json:
            return jsonify({"is_success": False, "error": "Invalid input: JSON expected."}), 400
        
        data = request.json.get("data")
        if not isinstance(data, list):
            return jsonify({"is_success": False, "error": "Invalid input: 'data' should be a list."}), 400
        
        numbers = [item for item in data if isinstance(item, str) and item.isdigit()]
        alphabets = [item for item in data if isinstance(item, str) and item.isalpha()]
        highest_alphabet = [max(alphabets, key=str.upper)] if alphabets else []
        
        response = {
            "is_success": True,
            "user_id": "lakshay_sharma_01012000",  # Replace with actual format
            "email": "your_email@domain.com",  # Replace with actual email
            "roll_number": "CU12345",  # Replace with actual roll number
            "numbers": numbers,
            "alphabets": alphabets,
            "highest_alphabet": highest_alphabet
        }
        return jsonify(response), 200
    except Exception as e:
        return jsonify({"is_success": False, "error": str(e)}), 500

@app.route('/bfhl', methods=['GET'])
def get_operation_code():
    return jsonify({"operation_code": 1}), 200

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=False, threaded=False)
