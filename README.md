# A ZeroMQ-based Communication Library
It cannot be used directly.
### 1. Installation
```bash
pip install pyzmq
pip install PagodaAL (If the package is not available in the mirror, run: pip install PagodaAL==0.1.0 -i https://pypi.org/simple)
```

### 2. Usage Instructions
#### 1) Import the PagodaAL Package as Follows
```python
from pagodaAL.zmqclass import ZmqManager
```

#### 2) Import the Log Package as Follows
```python
import logging
```

#### 3) Configure Logging
Logging is implemented to enhance code robustness and resilience. For the complete sample code, refer to the specific test documentation.
```python
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - ZmqManager - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)
```

#### 4) Create an Object Instance
Only the interfaces required by users are exposed. The `ip` refers to the bus IP, the receiving port is the bus REP port number, and the subscription port is the bus PUB port number.
```python
# Initialize the manager (IP, sender port, receiver port, subscription topics)
zmq_manager = ZmqManager(
    ip="127.0.0.1",
    sender_port=1111,
    receiver_port=2222,
    subscribe_topics=["test"]
)
```

#### 5) Send Messages
Users send messages that comply with the command specifications to the bus through this function.
```python
send_success = zmq_manager.send("test_message")
```

#### 6) Receive Messages
Users receive commands published by the bus (including status returns) through this function. The lifecycle of this function ends when its independent thread terminates—i.e., when the main thread terminates the independent thread of this function or the main function ends.
```python
received = zmq_manager.receive()
```
