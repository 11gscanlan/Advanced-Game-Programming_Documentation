# Task 6: Data Driven Movement System

The task for this week was creating a data-driven movement system

I didn't understand how to do this task, I tried my best but ultimately I gave up and, at the time, didn't ask for help. Not the best idea.

### Research

Structures in C++ (2019) At: https://www.geeksforgeeks.org/structures-in-cpp/ (Accessed  04/11/2024).


---
### Code

``` cpp
#include <iostream>
#include <vector>

// Struct for entity data (position and velocity)
struct EntityData
{
    float positionX;
    float positionY;
    float positionZ;
    float velocityX;
    float velocityY;
    float velocityZ;

    EntityData(float posX, float posY, float posZ, float velX, float velY, float velZ)
        : positionX(posX), positionY(posY), positionZ(posZ), velocityX(velX), velocityY(velY), velocityZ(velZ) {}
};

// Movement system class
class MovementSystem
{
public:
    // Store the entities' data in a vector
    std::vector<EntityData> entities;

    // Task for student: Implement this function to update the positions of all entities based on their velocities
    void UpdatePositions(float deltaTime)
    {
        for (size_t i = 0; i < entities.size(); ++i)
        {
            // Implement logic to update the positions of all entities using their velocity and deltaTime
            entities[i].positionX += entities[i].velocityX * deltaTime;
            entities[i].positionY += entities[i].velocityY * deltaTime;
            entities[i].positionZ += entities[i].velocityZ * deltaTime;
        }
    }

    // Function to print the positions of all entities
    void PrintPositions()
    {
        for (const auto& entity : entities)
        {
            std::cout << "Entity Position: X=" << entity.positionX << ", Y=" << entity.positionY
                      << ", Z=" << entity.positionZ << std::endl;
        }
    }
};

int main()
{
    // Initialize the MovementSystem and entities with sample data
    MovementSystem movementSystem;

    // Add some entities to the system
    movementSystem.entities.push_back(EntityData(0, 0, 0, 1, 0, 0));
    movementSystem.entities.push_back(EntityData(1, 2, 3, 0, 1, 0));
    movementSystem.entities.push_back(EntityData(5, 5, 5, 0, 0, 1));

    // Simulate multiple frames
    for (int frame = 0; frame < 5; ++frame)
    {
        std::cout << "\nFrame " << frame + 1 << std::endl;
        movementSystem.PrintPositions();    // Print current positions
        movementSystem.UpdatePositions(0.016f);  // Update positions with deltaTime (16ms per frame)
    }

    return 0;
}
```