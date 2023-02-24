# Debug-Interface-Kobuki
Debug interface for the kobuki robot using ros2 humble huskell. It uses the two available leds in all possible combinations and the speaker.

## How to debug
Using this debugging interface will allow you to use one of the following states avilables in this manual.

## How to install
Add in your package with the same folder structure as the example.

Copy the debug files.

Include the debug files in the nodes you want.

In the launcher add the remapping that the example launcher has.

## Use
### .h
  ```cpp
  // Publisher
  DebugNode::DebugPublisher debug_pub_;
  
  // Message
  DebugNode::DebugMessage debug_msg_;
  ```
### .cpp

  ```cpp

  // Init publisher
  debug_pub_ = create_publisher<DebugNode::DebugMessage>(DebugNode::TOPIC_NAME, 10);

  // Sent message
  debug_msg_.data = DebugNode::ERROR;  // Use whatever state you want
  debug_pub_->publish(debug_msg_);

  ```
