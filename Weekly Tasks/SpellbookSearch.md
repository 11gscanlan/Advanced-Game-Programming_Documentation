## Task 5: Spellbook Search


## Research

Developing A Basic Search Engine In C++: An Adventure In Coding - Code With C (2024) At: https://www.codewithc.com/developing-a-basic-search-engine-in-c/ (Accessed  28/10/2024).

---

The task for this week was to create a sorting algorithm that sorted a long list based on various criteria.


### Code Snippet
``` cpp
// Task for student: Implement a search function to find spells based on keywords
std::vector<Spell> SearchSpells(const std::vector<Spell>& spellList, const std::string& keyword)
{
    std::vector<Spell> results;
    for (const auto& spell : spellList)
    {


        // Check if the keyword matches the spell name, target type, or spell type
        std::string Name = spell.name;
        std::transform(Name.begin(), Name.end(), Name.begin(), ::toupper);

        if (Name.find(keyword) != std::string::npos ||
            spell.GetTargetTypeAsString().find(keyword) != std::string::npos ||
            spell.GetSpellTypeAsString().find(keyword) != std::string::npos)
        {
            results.push_back(spell);
        }
    }
    return results;
}
```
Whilst the code worked fine when you used uppercase words such as "Damage", it wouldn't work properly if you spelled it "damage". At the time I wanted to add a system to convert the text to lowercase but I didn't know how, and decided to instead continue working on my project as I had finished the task.

---
### Full Code:

``` cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

// Define the target types
enum class TargetType
{
    SingleTarget,
    AOE,
    Self
};

// Define the spell types
enum class SpellType
{
    Damage,
    Heal,
    Buff,
    Debuff
};

// The Spell class represents a single spell with attributes
class Spell
{
public:
    std::string name;
    int manaCost;
    int power;
    TargetType target;
    SpellType type;

    Spell(std::string n, int mCost, int p, TargetType t, SpellType st)
        : name(n), manaCost(mCost), power(p), target(t), type(st) {}

    void PrintSpell() const
    {
        std::cout << "Name: " << name << ", Mana Cost: " << manaCost
                  << ", Power: " << power << ", Target: " << GetTargetTypeAsString()
                  << ", Type: " << GetSpellTypeAsString() << std::endl;
    }

    std::string GetTargetTypeAsString() const
    {
        switch (target)
        {
        case TargetType::SingleTarget: return "Single Target";
        case TargetType::AOE: return "AOE";
        case TargetType::Self: return "Self";
        default: return "Unknown";
        }
    }

    std::string GetSpellTypeAsString() const
    {
        switch (type)
        {
        case SpellType::Damage: return "Damage";
        case SpellType::Heal: return "Heal";
        case SpellType::Buff: return "Buff";
        case SpellType::Debuff: return "Debuff";
        default: return "Unknown";
        }
    }
};

// Function to create a list of spells
std::vector<Spell> CreateSpells()
{
    return {
        {"Fireball", 50, 100, TargetType::SingleTarget, SpellType::Damage},
        {"Healing Aura", 30, 50, TargetType::AOE, SpellType::Heal},
        {"Shield", 20, 0, TargetType::Self, SpellType::Buff},
        {"Curse", 40, 60, TargetType::SingleTarget, SpellType::Debuff},
        {"Blizzard", 70, 80, TargetType::AOE, SpellType::Damage},
        {"Regenerate", 25, 30, TargetType::Self, SpellType::Heal},
        {"Lightning Strike", 55, 120, TargetType::SingleTarget, SpellType::Damage},
        {"Mass Shield", 60, 0, TargetType::AOE, SpellType::Buff},
        {"Flame Burst", 45, 110, TargetType::AOE, SpellType::Damage},
        {"Light Aura", 30, 0, TargetType::AOE, SpellType::Buff},
        {"Dark Curse", 40, 70, TargetType::SingleTarget, SpellType::Debuff},
        {"Water Wave", 35, 90, TargetType::AOE, SpellType::Damage},
        {"Thunderbolt", 60, 130, TargetType::SingleTarget, SpellType::Damage},
        {"Earthquake", 65, 150, TargetType::AOE, SpellType::Damage},
        {"Magic Barrier", 50, 0, TargetType::Self, SpellType::Buff},
        {"Invisibility", 30, 0, TargetType::Self, SpellType::Buff},
        {"Meteor Shower", 90, 200, TargetType::AOE, SpellType::Damage},
        {"Ice Spike", 35, 80, TargetType::SingleTarget, SpellType::Damage},
        {"Hurricane", 75, 140, TargetType::AOE, SpellType::Damage},
        {"Holy Light", 20, 40, TargetType::Self, SpellType::Heal},
        {"Lightning Storm", 80, 180, TargetType::AOE, SpellType::Damage},
        {"Sacred Flame", 60, 100, TargetType::SingleTarget, SpellType::Damage},
        {"Venom Strike", 30, 70, TargetType::SingleTarget, SpellType::Debuff},
        {"Frost Nova", 70, 90, TargetType::AOE, SpellType::Damage},
        {"Mana Shield", 40, 0, TargetType::Self, SpellType::Buff},
        {"Arcane Missiles", 45, 85, TargetType::SingleTarget, SpellType::Damage},
        {"Healing Rain", 35, 60, TargetType::AOE, SpellType::Heal},
        {"Divine Protection", 50, 0, TargetType::Self, SpellType::Buff},
        {"Poison Cloud", 50, 100, TargetType::AOE, SpellType::Debuff},
        {"Stone Skin", 25, 0, TargetType::Self, SpellType::Buff},
        {"Life Drain", 50, 70, TargetType::SingleTarget, SpellType::Debuff},
        {"Phoenix Fire", 100, 250, TargetType::AOE, SpellType::Damage},
        {"Raging Inferno", 90, 210, TargetType::AOE, SpellType::Damage},
        {"Whirlwind", 55, 85, TargetType::AOE, SpellType::Damage},
        {"Blessing of Light", 30, 0, TargetType::Self, SpellType::Buff},
        {"Shadow Bolt", 40, 90, TargetType::SingleTarget, SpellType::Damage},
        {"Serpent's Bite", 45, 65, TargetType::SingleTarget, SpellType::Debuff},
        {"Cleansing Wave", 25, 0, TargetType::AOE, SpellType::Heal},
        {"Chill Touch", 35, 50, TargetType::SingleTarget, SpellType::Damage},
        {"Blood Pact", 60, 0, TargetType::Self, SpellType::Buff},
        {"Lunar Strike", 75, 160, TargetType::SingleTarget, SpellType::Damage},
        {"Solar Flare", 65, 140, TargetType::AOE, SpellType::Damage},
        {"Nature's Grasp", 50, 80, TargetType::SingleTarget, SpellType::Buff},
        {"Wrath of the Ancients", 100, 250, TargetType::AOE, SpellType::Damage},
        {"Ethereal Form", 40, 0, TargetType::Self, SpellType::Buff},
        {"Radiant Heal", 30, 70, TargetType::SingleTarget, SpellType::Heal},
        {"Stormcall", 80, 150, TargetType::AOE, SpellType::Damage},
        {"Chain Lightning", 70, 130, TargetType::AOE, SpellType::Damage},
        {"Ice Dash", 25, 15, TargetType::Self, SpellType::Damage},
    };
}

// Task for student: Implement a search function to find spells based on keywords
std::vector<Spell> SearchSpells(const std::vector<Spell>& spellList, const std::string& keyword)
{
    std::vector<Spell> results;
    for (const auto& spell : spellList)
    {


        // Check if the keyword matches the spell name, target type, or spell type
        std::string Name = spell.name;
        std::transform(Name.begin(), Name.end(), Name.begin(), ::toupper);

        if (Name.find(keyword) != std::string::npos ||
            spell.GetTargetTypeAsString().find(keyword) != std::string::npos ||
            spell.GetSpellTypeAsString().find(keyword) != std::string::npos)
        {
            results.push_back(spell);
        }
    }
    return results;
}



int main()
{
    std::vector<Spell> spells = CreateSpells();

    std::string keyword;
    std::cout << "Search terms: Damage, Heal, Buff, Debuff, SingleTarget, AOE, Self" << std::endl;
    std::cout << "Enter a search keyword:" << std::endl;
    std::getline(std::cin, keyword);

    // Search for spells based on the keyword
    std::vector<Spell> matchingSpells = SearchSpells(spells, keyword);

    // Display the results
    if (!matchingSpells.empty())
    {
        std::cout << "Matching Spells:" << std::endl;
        for (const auto& spell : matchingSpells)
        {
            spell.PrintSpell();
        }
    }
    else
    {
        std::cout << "No spells matched the search criteria." << std::endl;
    }

    return 0;
}

```