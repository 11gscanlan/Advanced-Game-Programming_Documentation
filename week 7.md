# Week 7

## Class Task

***Some parts of the code is me recreating them from memory, as the end result changed quite a bit from the start point***

Our task for this week was to create a character creation system using factory creation.
I was paired with Zoy, and we got some help from Ross who was sat next to me and felt like helping while his project was being very uncooperative with his procedural generation.

We started by creating the class initialization, where each class has specific stats. We started off with a Switch case algorithm where each case was the different classes; Warrior, Mage, Wizard, etc.

After entering the first case for Warrior, we decided to open ChatGPT and ask it to generate the rest of the switch cases as that way we wouldn't have to repeat the code 8 more times, which helped save a lot of time as it not only made the rest of the switch cases, but also randomised the values too.

``` cpp
switch (characterClass) {
 case characterClass::Warrior
 character.strength = 10
 character.agility = 8
 character.endurance = 9
 character.intelligence = 7
 character.willpower = 6
 character.speed = 5
 character.luck = 4
}
```

From there we wanted to test that the code worked, so wanted to create the function that outputted the selection of our chosen class along with its stats.
Our first character was a Mage named "Steve".

``` cpp
Character* warrior = CharacterFactory::CreateCharacter("Steve", CharacterClass::Warrior);
	
std::cout << "Character Info:" << std::endl;
warrior->PrintCharacterInfo();
```
Where "Print Character Info" was defined as:

``` cpp
    virtual void PrintCharacterInfo()
    {
        std::cout << "Name: " << name << ", Class: " << static_cast<int>(characterClass) << std::endl;
        std::cout << "Strength: " << strength << ", Agility: " << agility
                  << ", Endurance: " << endurance << ", Intelligence: " << intelligence
                  << ", Willpower: " << willpower << ", Speed: " << speed
                  << ", Luck: " << luck << std::endl;
    }
```
Therefore it would return;
*Character Info:
"Name: Steve", "2" Strength 10", Agility 8", Endurance: 9", "Intelligence: 7", "Willpower: 6", "Speed 5", "Luck: 4"

We almost immediately noticed that the class was being returned as **2** and not **Mage**, as the initial code was
***static_cast<int>(characterClass)***, which meant it was getting the array value as an integer, and not a string.
We then attempted to brute force different methods to try and get the class to display as a string, to no avail.
We once again asked ChatGPT how we could go about converting the array element into a string instead of an integer. It told us to create a seperate function that we call instead that gets the array element and converts the value to a string, so we created the function **toString** with help from ChatGPT.

``` cpp
// Function to convert enum to string
std::string toString(CharacterClass characterClass) {
	switch (characterClass) {
	case CharacterClass::Warrior:
		return "Warrior";
	case CharacterClass::Rogue:
		return "Rogue";
	case CharacterClass::Mage:
		return "Mage";
	case CharacterClass::Wizard:
		return "Wizard";
	case CharacterClass::Ranger:
		return "Ranger";
	case CharacterClass::Monk:
		return "Monk";
	case CharacterClass::Bard:
		return "Bard";
	case CharacterClass::Paladin:
		return "Paladin";
	case CharacterClass::Cleric:
		return "Cleric";
	default:
		return "Unknown";
	}
}
```
After that we swapped the ***static_cast<int>(characterClass)*** to instead be ***toString(characterClass)***. Which changed the output to **Mage** instead of **2**.



After that we asked ChatGPT to see if there was a way to simplify the method for calculating the stats, as having 9 tabs of stats was taking up about 50 lines of code.

ChatGPT told us that we could simplify the code by instead using an array for each class that stores the stats,
and then when retrieving the stats it finds the specific value in the array.

``` cpp
const std::map<CharacterClass, std::vector<int>> CharacterFactory::classStats = {
	{CharacterClass::Warrior, {10, 8, 9, 7, 6, 5, 4}},
	{CharacterClass::Rogue, {7, 10, 6, 8, 6, 9, 8}},
	{CharacterClass::Mage, {5, 6, 6, 10, 7, 6, 5}},
	{CharacterClass::Wizard, {4, 5, 6, 10, 8, 4, 6}},
	{CharacterClass::Ranger, {8, 9, 7, 7, 6, 8, 7}},
	{CharacterClass::Monk, {8, 8, 9, 7, 9, 7, 5}},
	{CharacterClass::Bard, {6, 7, 6, 8, 6, 7, 10}},
	{CharacterClass::Paladin, {9, 7, 10, 7, 9, 6, 5}},
	{CharacterClass::Cleric, {5, 5, 7, 8, 9, 4, 7}}
};
```
## Cleanup Causing the decorators to be generated. Oops.

``` cpp
int main()
{
    // Create characters using the factory
    Character* warrior = CharacterFactory::CreateCharacter("Steve", CharacterClass::Warrior);
    Character* bard = CharacterFactory::CreateCharacter("Herobrine", CharacterClass::Bard);

    // Apply decorators to modify characters
    Character* warriorWithArmor = new EnchantedArmorDecorator(warrior);
    Character* bardWithWeapon = new SpecialWeaponDecorator(bard);

    // Print character information
    std::cout << "\nWarrior Info with Enchanted Armor:" << std::endl;
    warriorWithArmor->PrintCharacterInfo();
    
    std::cout << "\nWarrior Info without Enchanted Armor:" << std::endl;
    warrior->PrintCharacterInfo();

    std::cout << "\nBard Info with Special Weapon:" << std::endl;
    bardWithWeapon->PrintCharacterInfo();

    // Cleanup
    delete warrior;
    delete bard;
    delete warriorWithArmor;
    delete bardWithWeapon;

    return 0;
}
```

After that Zoe decided to tinker with some things, and asked ChatGPT to clean up the code, making it less messy, as well as adding player configuration to the functions, meaning the player can select their own class, name, and additional decorator equipment at runtime.
I left to go to the toilet at this time, so I wasn't there for most of it, but Zoe explained what had changed when I got back so I understood the changes.
After that, we tried a few tests, and added some failsafes incase the player inputs the wrong value to prevent errors, then after that, the task was complete.

### Full Code:
``` cpp
#include <iostream>
#include <string>
#include <map>
#include <vector>
#include <memory>

// Define the character classes
enum class CharacterClass
{
	Warrior,
	Rogue,
	Mage,
	Wizard,
	Ranger,
	Monk,
	Bard,
	Paladin,
	Cleric
};

// Function to convert enum to string
std::string toString(CharacterClass characterClass) {
	switch (characterClass) {
	case CharacterClass::Warrior:
		return "Warrior";
	case CharacterClass::Rogue:
		return "Rogue";
	case CharacterClass::Mage:
		return "Mage";
	case CharacterClass::Wizard:
		return "Wizard";
	case CharacterClass::Ranger:
		return "Ranger";
	case CharacterClass::Monk:
		return "Monk";
	case CharacterClass::Bard:
		return "Bard";
	case CharacterClass::Paladin:
		return "Paladin";
	case CharacterClass::Cleric:
		return "Cleric";
	default:
		return "Unknown";
	}
}

// Character base class
class Character
{
public:
	std::string name;
	CharacterClass characterClass;
	int strength, agility, endurance, intelligence, willpower, speed, luck;

	Character(std::string n, CharacterClass c)
		: name(n), characterClass(c), strength(5), agility(5), endurance(5),
		  intelligence(5), willpower(5), speed(5), luck(5) {}

	virtual void PrintCharacterInfo() {
		std::cout << "Name: " << name << ", Class: " << toString(characterClass) << std::endl;
		std::cout << "Strength: " << strength << ", Agility: " << agility
		          << ", Endurance: " << endurance << ", Intelligence: " << intelligence
		          << ", Willpower: " << willpower << ", Speed: " << speed
		          << ", Luck: " << luck << std::endl;
	}

	virtual ~Character() = default;
};

// Character Factory
class CharacterFactory
{
private:
	static const std::map<CharacterClass, std::vector<int>> classStats;

public:
	static std::unique_ptr<Character> CreateCharacter(const std::string& name, CharacterClass charClass)
	{
		auto it = classStats.find(charClass);
		if (it == classStats.end()) {
			std::cout << "Invalid character class!" << std::endl;
			return nullptr;
		}

		// Use direct std::unique_ptr construction instead of std::make_unique (C++11 compatibility)
		std::unique_ptr<Character> character(new Character(name, charClass));
		const std::vector<int>& stats = it->second;

		character->strength = stats[0];
		character->agility = stats[1];
		character->endurance = stats[2];
		character->intelligence = stats[3];
		character->willpower = stats[4];
		character->speed = stats[5];
		character->luck = stats[6];

		return character;
	}

	static void ShowClassStats(CharacterClass charClass)
	{
		auto it = classStats.find(charClass);
		if (it != classStats.end()) {
			const auto& stats = it->second;
			std::cout << "Stats for " << toString(charClass) << ":\n";
			std::cout << "Strength: " << stats[0] << "\n";
			std::cout << "Agility: " << stats[1] << "\n";
			std::cout << "Endurance: " << stats[2] << "\n";
			std::cout << "Intelligence: " << stats[3] << "\n";
			std::cout << "Willpower: " << stats[4] << "\n";
			std::cout << "Speed: " << stats[5] << "\n";
			std::cout << "Luck: " << stats[6] << "\n";
		}
	}

	static void ShowClassList()
	{
		std::cout << "Available Character Classes:\n";
		std::cout << "0. Warrior\n1. Rogue\n2. Mage\n3. Wizard\n4. Ranger\n5. Monk\n6. Bard\n7. Paladin\n8. Cleric\n";

	};
};

// Static initialization of the classStats map
const std::map<CharacterClass, std::vector<int>> CharacterFactory::classStats = {
	{CharacterClass::Warrior, {10, 8, 9, 7, 6, 5, 4}},
	{CharacterClass::Rogue, {7, 10, 6, 8, 6, 9, 8}},
	{CharacterClass::Mage, {5, 6, 6, 10, 7, 6, 5}},
	{CharacterClass::Wizard, {4, 5, 6, 10, 8, 4, 6}},
	{CharacterClass::Ranger, {8, 9, 7, 7, 6, 8, 7}},
	{CharacterClass::Monk, {8, 8, 9, 7, 9, 7, 5}},
	{CharacterClass::Bard, {6, 7, 6, 8, 6, 7, 10}},
	{CharacterClass::Paladin, {9, 7, 10, 7, 9, 6, 5}},
	{CharacterClass::Cleric, {5, 5, 7, 8, 9, 4, 7}}
};

// Decorator for adding abilities or modifiers to characters
class CharacterDecorator : public Character
{
protected:
	std::unique_ptr<Character> character;

public:
	CharacterDecorator(std::unique_ptr<Character> c) : Character(c->name, c->characterClass), character(std::move(c)) {}

	virtual void PrintCharacterInfo() override {
		character->PrintCharacterInfo();
	}
};

// Concrete Decorator: EnchantedArmor (for example)
class EnchantedArmorDecorator : public CharacterDecorator
{
public:
	EnchantedArmorDecorator(std::unique_ptr<Character> c) : CharacterDecorator(std::move(c)) {}

	void PrintCharacterInfo() override {
		character->PrintCharacterInfo();
		std::cout << "Equipped with Enchanted Armor: +2 Strength, +1 Endurance" << std::endl;
		character->strength += 2;
		character->endurance += 1;
	}
};

// Concrete Decorator: SpecialWeapon (for example)
class SpecialWeaponDecorator : public CharacterDecorator
{
public:
	SpecialWeaponDecorator(std::unique_ptr<Character> c) : CharacterDecorator(std::move(c)) {}

	void PrintCharacterInfo() override {
		character->PrintCharacterInfo();
		std::cout << "Equipped with Special Weapon: +3 Agility, +2 Luck" << std::endl;
		character->agility += 3;
		character->luck += 2;
	}
};

int main() {
	// Show available classes
	CharacterFactory::ShowClassList();
	std::cout << "Choose a character class by number:\n";
	int classChoice;
	std::cin >> classChoice;

	std::cout << "Enter the name of your character: ";
	std::string name;
	std::cin >> name;



	if (classChoice < 0 || classChoice >= 9) {
		std::cout << "Invalid choice. Exiting.\n";
		return 1;
	}

	CharacterClass chosenClass = static_cast<CharacterClass>(classChoice);
	std::unique_ptr<Character> character = CharacterFactory::CreateCharacter(name, chosenClass);

	// Show character stats
	CharacterFactory::ShowClassStats(chosenClass);

	std::cout << "Do you want to equip any items? (y/n): ";
	char equipChoice;
	std::cin >> equipChoice;

	if (equipChoice == 'y' || equipChoice == 'Y') {
		std::cout << "Choose an item to equip:\n";
		std::cout << "1. Enchanted Armor (+2 Strength, +1 Endurance)\n";
		std::cout << "2. Special Weapon (+3 Agility, +2 Luck)\n";
		int itemChoice;
		std::cin >> itemChoice;

		if (itemChoice == 1) {
			character = std::unique_ptr<EnchantedArmorDecorator>(new EnchantedArmorDecorator(std::move(character)));
		} else if (itemChoice == 2) {
			character = std::unique_ptr<SpecialWeaponDecorator>(new SpecialWeaponDecorator(std::move(character)));
		}
	}

	std::cout << "\nCharacter Info:\n";
	character->PrintCharacterInfo();

	return 0;
}

```

## Prototype Development

### Door

### Inventory System