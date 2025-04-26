# optimization-
About the optimization API design
from flask import Flask, request, jsonify
import time
import random

app = Flask(__name__)

def optimize_container_routing(containers):
    # A simple mock optimization algorithm
    # In a real scenario, you would replace this with your actual optimization logic
    optimized_plan = sorted(containers, key=lambda x: x['destination'])
    return optimized_plan

@app.route('/optimize', methods=['POST'])
def optimize():
    start_time = time.time()
    
    data = request.json
    if 'containers' not in data:
        return jsonify({'error': 'No containers provided'}), 400
    
    containers = data['containers']
    
    # Call the optimization function
    optimized_plan = optimize_container_routing(containers)
    
    latency = time.time() - start_time
    return jsonify({
        'optimized_plan': optimized_plan,
        'latency': latency
    })

if __name__ == '__main__':
    app.run(debug=True)
