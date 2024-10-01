https://www.geeksforgeeks.org/bubble-sort-in-cpp/ (accessed 1/10/2024)

https://chatgpt.com/ (accessed 1/10/2024)

Used to explain bubble sorting in cpp, as well as to generate a cheat sheet for cpp to help me understand it better

## Development Process:


### Challenges
One of the main challenges I faced was the difficulty I have with my understanding of C++, therefore I needed to also spend time researching the basics of C++ to help with my understanding of what to do.

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

class Item
{
public:
    std::string name;
    int value;
    
    Item(std::string n, int v) : name(n), value(v) {}

};

// Function to display the inventory
void DisplayInventory(const std::vector<Item>& items)
{
    for (const auto& item : items)
    {
        std::cout << item.name << ": " << item.value << std::endl;
    }
}


// Function to sort items by name (alphabetically)
void SortByName(std::vector<Item>& items, bool ascending = true)
{
    int n = items.size();
    if (ascending)
        
        // For loop that corresponds to the number of items that need to be sorted
        for (int i = 0; i < n - 1; i++) {
            // Last i elements are already in place
            for (int j = 0; j < n - i - 1; j++) {
                // Comparing adjacent elements
                if (items[j].name > items[j + 1].name)
                    // Swap items if in the wrong order
                    std::swap(items[j], items[j + 1]);
                
            }
        } 
    else
        for (int i = 0; i < n - 1; i++) {
            // Last i elements are already in place
            for (int j = 0; j < n - i - 1; j++) {
                // Comparing adjacent elements
                if (items[j].name < items[j + 1].name)
                    // Swap items if in the wrong order
                    std::swap(items[j], items[j + 1]);
            }
        }
         
}

// Function that sorts by value, if true then sort ascending
void SortByValue(std::vector<Item>& items, bool ascending = true)
{
    int v = items.size();
    if (ascending)
        
        // For loop that corresponds to the number of items that need to be sorted
        for (int i = 0; i < v - 1; i++) {
            // Last i elements are already in place
            for (int j = 0; j < v - i - 1; j++) {
                // Comparing adjacent elements
                if (items[j].value > items[j + 1].value)
                    // Swap items if in the wrong order
                    std::swap(items[j], items[j + 1]);
                
            }
        } 
// Else, sort descending
    else
        for (int i = 0; i < v - 1; i++) {
            // Last i elements are already in place
            for (int j = 0; j < v - i - 1; j++) {
                // Comparing adjacent elements
                if (items[j].value < items[j + 1].value)
                    // Swap items if in the wrong order
                    std::swap(items[j], items[j + 1]);
            }
        }
         
}




int main()
{
    std::vector<Item> items = {
        Item("Sword", 150),
        Item("Potion", 50),
        Item("Shield", 100),
        Item("Bow", 120),
        Item("Helmet", 80),
        Item("My diamond sword-sword you can't afford-ford my diamond sword-sword", 6969)
    };

    std::cout << "Original Inventory:" << std::endl;
    DisplayInventory(items);
    
    std::string userInput;
    
    // Prompt the user for input
    std::cout << "Would you like to sort your inventory by 'name' or 'value'?";
    std::getline(std::cin, userInput);
    
    // Check the input using if, else if, or else
    if (userInput == "name") {
        
        std::cout << "Would you like the list to be 'ascending' or 'descending'?";
        std::getline(std::cin, userInput);
        
        if (userInput == "ascending") {
            std::cout << "\nSorted by Name (Ascending):" << std::endl;
            SortByName(items, true); // Sort by name in ascending order
            DisplayInventory(items);
            
        } else if (userInput == "descending") {
            std::cout << "\nSorted by Name (Descending):" << std::endl;
            SortByName(items, false); // Sort by name in descending order
            DisplayInventory(items); 
            
        } else {
            std::cout << "Sorry, I don't understand that command :(" << std::endl;
        }
    } else {
        std::cout << "Would you like the list to be 'ascending' or 'descending'?";
        std::getline(std::cin, userInput);
        
        if (userInput == "ascending") {
            std::cout << "\nSorted by Name (Ascending):" << std::endl;
            SortByValue(items, true); // Sort by name in ascending order
            DisplayInventory(items);
            
        } else if (userInput == "descending") {
            std::cout << "\nSorted by Name (Descending):" << std::endl;
            SortByValue(items, false); // Sort by name in descending order
            DisplayInventory(items); 
            
        } else {
            std::cout << "Sorry, I don't understand that command :(" << std::endl;
    }
    }
    
    return 0;
}
```