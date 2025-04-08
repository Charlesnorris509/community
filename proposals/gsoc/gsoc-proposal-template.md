# Project Title

Project #23: Structured Parameter Support for ROS 2

## Summary

The Structured Parameter Support for ROS 2 project addresses a significant limitation in the current ROS 2 parameter system, which only supports primitive types and arrays. This restricts the flexibility and expressiveness of configuration options for ROS 2 applications.
My proposed solution extends the parameter system to support complex data structures through YAML serialization, enabling developers to use structured parameters that can represent hierarchical configurations. This implementation will maintain backward compatibility while providing an intuitive API for working with these structured parameters.
The anticipated impact is substantial: ROS 2 developers will gain more powerful configuration capabilities, reducing boilerplate code, improving code organization, and enabling more sophisticated robot behaviors through richer configuration options.

## Personal Information

- **Full Name**: Charles Alexandre C. Norris
- **Email Address**: cnorris7@gmu.edu
- **GitHub Profile**: https://github.com/Charlesnorris509
- **LinkedIn**: https://linkedin.com/in/charlesanorris
- **University/College**: George Mason Univeristy
- **Degree Program**: Information Technology
- **Year of Study**: Senior
- **Country of Residence**: United States of America
- **Timezone**: Eastern standard time

## Qualifications; Motivation?

I bring a strong technical foundation and relevant experience that make me well-suited for implementing Structured Parameter Support for ROS 2. As a senior Information Technology student at George Mason University with a concentration in Data Technology and Programming, I have hands-on experience designing scalable applications, conducting penetration testing, and contributing to open-source projects including Laravel, DocsGPT, and Kubernetes.
My technical qualifications include:
Proficiency in C++ and software engineering principles
Experience with database programming and cloud computing
AWS Cloud Practitioner Certification and Microsoft Certified Power Platform Fundamentals
Software Engineer Intern experience at GMU's College of Engineering and Computing
Teaching Assistant role demonstrating strong communication and mentoring abilities
Selected for the competitive Amazon NeXT Scholar Program
I have contributed to open-source projects where I've honed my ability to troubleshoot complex problems, optimize system performance, and enhance software reliability. My experience with template metaprogramming and serialization techniques will be particularly valuable for implementing the core functionality of this project.
I commit to dedicating 35-40 hours per week to this project throughout the GSoC period. As a student, my academic commitments are minimal during the summer, allowing me to focus primarily on this project. I have no planned vacations or major conflicts during the coding period. Should any unexpected academic obligations arise, I will manage them by adjusting my daily schedule while maintaining my weekly hour commitment.
My motivation for working on this project stems from my belief that great engineering isn't just about technical acumen but about solving real problems and improving developer experiences. The current limitation in ROS 2's parameter system represents a practical challenge that, when solved, will significantly enhance the framework's capabilities. I'm excited by the opportunity to contribute to the ROS 2 ecosystem, which is widely used in robotics research and industry applications. This project aligns perfectly with my interests in systems programming and API design, while allowing me to make a meaningful contribution to a technology that powers cutting-edge robotics applications.

## Goals

Extend the ParameterValue message definition to include a new field for structured data (YAML-serialized structure)
Update the Parameter Type enumeration to include the new structured type
Modify rclcpp library to handle the new parameter type with proper validation
Implement a template-based serialization/deserialization system between C++ structs and YAML
Create convenience functions for converting between ROS messages and structured parameters
Develop a YAML template generation tool to facilitate configuration file creation
Create comprehensive documentation and tutorials for using structured parameters
Implement thorough unit and integration tests to ensure reliability
Provide example code demonstrating usage in real-world scenarios

## Non-Goals

This project will not modify existing parameter types or their behavior, ensuring backward compatibility
The implementation will not extend to languages other than C++ in this initial phase
This project will not include a graphical user interface for editing structured parameters
The implementation will not support direct serialization of arbitrary classes with methods, focusing only on data structures
This project will not implement automatic conversion between different message types
Performance optimization beyond reasonable efficiency is not a primary goal for this initial implementation

## Technical Details

The implementation of Structured Parameter Support for ROS 2 involves several technical components:
Modifying ParameterValue Message: I will extend the ParameterValue message definition in rcl_interfaces/msg/ParameterValue.msg to include a new field for structured data:

# Existing fields
<pre> ``` 
byte type
bool bool_value
int64 integer_value
float64 double_value
string string_value
array bool bool_array_value
array int64 integer_array_value
array float64 double_array_value
array string string_array_value
``` </pre>

# New field for structured parameters
string yaml_value # YAML-serialized structure
Updating Parameter Type Enumeration: The parameter type enumeration in rcl_interfaces/msg/ParameterType.msg will be extended to include the new structured type:

<pre> ```
uint8 PARAMETER_NOT_SET=0
uint8 PARAMETER_BOOL=1
uint8 PARAMETER_INTEGER=2
uint8 PARAMETER_DOUBLE=3
uint8 PARAMETER_STRING=4
uint8 PARAMETER_BOOL_ARRAY=5
uint8 PARAMETER_INTEGER_ARRAY=6
uint8 PARAMETER_DOUBLE_ARRAY=7
uint8 PARAMETER_STRING_ARRAY=8
uint8 PARAMETER_STRUCTURED=9 # New type
``` </pre>

Modifying rclcpp Parameter Handling: The rclcpp library will be updated to handle the new parameter type:
• Modify rclcpp::ParameterValue to support the new structured type
• Update parameter validation to accept structured parameters
• Implement serialization/deserialization between C++ structs and YAML

Implementing Serialization/Deserialization: The core of this project is the serialization/deserialization mechanism:
• A template-based system for converting C++ structs to YAML
• A mechanism to convert YAML back to C++ structs
• Validation to ensure the YAML structure matches the expected C++ struct
I'll leverage the yaml-cpp library and implement template metaprogramming techniques to automatically traverse struct members.
- ROS Message Integration: To simplify usage, I'll implement convenience functions to convert between ROS messages and structured parameters, leveraging ROS messages' built-in introspection feature.
- YAML Template Generation Tool: As a stretch goal, I'll implement a command-line tool to generate YAML templates from ROS message definitions:
<pre> ``` ros2 param template my_package/msg/MyConfig > my_config_template.yaml ``` </pre>
Potential challenges include:
• Ensuring proper handling of complex nested structures
• Maintaining backward compatibility
• Providing clear error messages for validation failures
• Handling different YAML serialization formats

I plan to address these challenges through careful API design, comprehensive testing, and regular feedback from mentors and the ROS 2 community.

## Test Plan

My testing strategy will ensure the reliability and correctness of the Structured Parameter Support implementation:
Unit Tests:
Test serialization/deserialization of various struct types (simple, nested, with arrays)
Test parameter validation for structured parameters
Test error handling for malformed YAML or type mismatches
Test conversion between ROS messages and structured parameters
Integration Tests:
Create test nodes that use structured parameters in realistic scenarios
Test parameter updates and callbacks with structured parameters
Test interaction with parameter services and parameter client
Test loading structured parameters from YAML files
Compatibility Tests:
Verify that existing code using primitive parameters continues to work
Test mixed use of primitive and structured parameters
Test parameter introspection tools with structured parameters
Performance Tests:
Benchmark serialization/deserialization operations
Compare memory usage with equivalent primitive parameter approaches
I will use the standard ROS 2 testing frameworks (gtest, launch testing) and aim for high test coverage. All tests will be automated and integrated into the CI pipeline to ensure ongoing reliability.

## Estimation of Deliverables

- **Milestone 1**: Community Bonding Period (May 1 - May 28, 2025)
• Engage with the ROS 2 community to refine the project scope
• Set up development environment and familiarize with the codebase
• Study existing parameter implementation in detail
• Create detailed design document for review by mentors

- **Milestone 2**:Basic Parameter Type Implementation (May 29 - June 11, 2025)
• Implement modifications to ParameterValue message
• Update parameter type enumeration
• Create initial tests for the new parameter type
• Deliverable: Basic structured parameter type definition complete
  
- **Milestone 3**: Serialization Implementation (June 12 - June 25, 2025)
• Implement YAML serialization/deserialization for basic struct types
• Modify rclcpp to handle structured parameters
• Create unit tests for serialization/deserialization
• Deliverable: Basic serialization/deserialization working

- **Milestone 4**: Advanced Features (June 26 - July 9, 2025)
• Implement nested struct support
• Add support for arrays of structs
• Enhance error handling and validation
• Deliverable: Complete structured parameter implementation

- **Milestone 5**:  ROS Integration (July 10 - July 23, 2025)
• Implement convenience methods for ROS message conversion
• Create integration tests with real-world examples
• Begin documentation
• Deliverable: ROS message integration complete

- **Milestone 6**: Finalization (July 24 - August 6, 2025)
• Implement YAML template generation tool
• Create comprehensive examples
• Complete documentation and tutorials
• Final testing and bug fixes
• Deliverable: YAML template tool complete and project finalized


## Additional Notes (Optional)

I'm excited about the potential impact of this project on the ROS 2 ecosystem. Structured parameters will enable more sophisticated configuration options for robotics applications, reducing the need for custom parameter handling code and improving the overall developer experience.
I've already begun exploring the ROS 2 parameter system implementation and am confident that the proposed approach is feasible within the GSoC timeframe. I look forward to collaborating with mentors and the community to refine the design and ensure it meets the needs of ROS 2 users.





