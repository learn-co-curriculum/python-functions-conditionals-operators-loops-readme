
# Conditionals, Loops, Operators, Functions: Bringing It All Together

We've learned about a lot of statements we have available to us in Python to write more dynamic and concise code. Conditionals let us create *conditions* that inform our code how to operate. Loops help us to dynamically iterate through and operate on a collection (i.e. a list or a dictionary). And Operators, generally, allow us to compare elements to each other, assert the sameness of elements, or return elements based on their truthiness or falsiness. Functions, essentially, help us to create an object that packages up one or more operations and allows us to execute those operations from anywhere else in scope in our code. However, as we can tell by the title of this lesson, we will now be focusing on using all of these smaller parts together. As we get further into our lives as programmers, we will find ourselves facing more and more complex problems and to solve those we will need these types of tools to create solutions while keeping our code concise and efficient. 

## Objectives:
* Understand how and when to use functions, conditionals, loops, and operators in tandem

## Bringing It All Together

The best way to understand how and when to use all these parts in a whole is to use an example. So, we are going to use data from a basketball game with 2 teams; the away team and the home team. We'll assing this data to a variable called `game_data` and use it in the examples below where we will create functions that operate on this data to retrieve information about the teams and players.

This data structure is a bit complicated, so, make sure to look it over and get familiar with it.


```python
game_data = { 
"home": {
    "team_name": "Brooklyn Nets",
    "colors": ["Black", "White"],
    "players": {
      "Alan Anderson": {
        "number": 0,
        "shoe": 16,
        "points": 22,
        "rebounds": 12,
        "assists": 12,
        "steals": 3,
        "blocks": 1,
        "slam_dunks": 1
      },
      "Reggie Evans": {
        "number": 30,
        "shoe": 14,
        "points": 12,
        "rebounds": 12,
        "assists": 12,
        "steals": 12,
        "blocks": 12,
        "slam_dunks": 7
      },
      "Brook Lopez": {
        "number": 11,
        "shoe": 17,
        "points": 17,
        "rebounds": 19,
        "assists": 10,
        "steals": 3,
        "blocks": 1,
        "slam_dunks": 15
      },
      "Mason Plumlee": {
        "number": 1,
        "shoe": 19,
        "points": 26,
        "rebounds": 12,
        "assists": 6,
        "steals": 3,
        "blocks": 8,
        "slam_dunks": 5
      },
      "Jason Terry": {
        "number": 31,
        "shoe": 15,
        "points": 19,
        "rebounds": 2,
        "assists": 2,
        "steals": 4,
        "blocks": 11,
        "slam_dunks": 1
      }
    }
  },
  "away": {
    "team_name": "Charlotte Hornets",
    "colors": ["Turquoise", "Purple"],
    "players": {
      "Jeff Adrien": {
        "number": 4,
        "shoe": 18,
        "points": 10,
        "rebounds": 1,
        "assists": 1,
        "steals": 2,
        "blocks": 7,
        "slam_dunks": 2
      },
      "Bismak Biyombo": {
        "number": 0,
        "shoe": 16,
        "points": 12,
        "rebounds": 4,
        "assists": 7,
        "steals": 7,
        "blocks": 15,
        "slam_dunks": 10
      },
      "DeSagna Diop": {
        "number": 2,
        "shoe": 14,
        "points": 24,
        "rebounds": 12,
        "assists": 12,
        "steals": 4,
        "blocks": 5,
        "slam_dunks": 5
      },
      "Ben Gordon": {
        "number": 8,
        "shoe": 15,
        "points": 33,
        "rebounds": 3,
        "assists": 2,
        "steals": 1,
        "blocks": 1,
        "slam_dunks": 0
      },
      "Brendan Haywood": {
        "number": 33,
        "shoe": 15,
        "points": 6,
        "rebounds": 12,
        "assists": 12,
        "steals": 22,
        "blocks": 5,
        "slam_dunks": 12
      }
    }
  }
}

```

There's a lot of information here and it's all contained in a pretty organized, but otherwise nested structure. So, let's start out with a straightforward example of getting a list of the colors for both teams.

We want to return a **single** list with the strings for each color for both the home and away teams. We know that we want something from **both** teams, so, we will need to iterate over the `game_data` object, which is a dictionary. So, we will iterate using its **keys** and **values**, but we know that the `'colors'` attribute points to a *list*, so, we will need to iterate over that as well to access each color individually and append it to our *new* list of colors, which we will then return at the end of the function. Let's take a look at this implementation.


```python
def get_colors(game_dict):
    # we create a new list to hold the strings for each color for both the home and away teams
    all_colors = []
    # then we iterate over the dictionary to access the data for each team
    for team, team_data in game_dict.items():
        # once we have access to the data for a team, we then iterate over its list of colors
        for color in team_data['colors']:
            # then we append each color to our new list
            all_colors.append(color)
    # finally, we return our new list which should contain every color for both teams
    return all_colors
```


```python
get_colors(game_data)
```

So, to recap, in the above example we saw that we would have to use a **nested** loop because we were dealing with a **nested** data structure (e.g. a dictionary, which points to another dictionary, which then points to a list).

In the next cell, we will define a method that retrieves the names of all players from whichever `'team_name'` is passed in. So, if we want to see the players on the charlotte hornets, we would give, as the second argument, `"charlotte hornets"`. However, if there is no second argument given, we should return a list with **all** the players.


```python
def get_players(game_dict, team_name=None):
    players = []
    if team_name is not None:
        for team, team_data in game_dict.items():
            if team_name.lower() == team_data['team_name'].lower():
                for player in team_data['players']:
                    players.append(player)
    else:
        for team, team_data in game_dict.items():
            for player in team_data['players']:
                players.append(player)
    return players
```


```python
get_players(game_data)
```


```python
get_players(game_data, 'charlotte hornets')
```

In this example, again we were dealing with a nested data structure, so, we had to have a nested loop. We *also* introduced a **condition** to our problem. We wanted to return one list **if** we were given a team name and another list **if** we were **not** given a team name. And to make sure we would get the correct players in the case that there is a team name, we had to check that the team name that was passed in as the second argument was **equal to** the `'team_name'` value of the given dictionary.

## Summary

With the above examples, we can see that deciding when to use functions, condtionals, operators, and loops all depends on the problem at hand. We can use context clues to give us a good idea of the structure our solution will take. If we have a condtion that would change the output of our return value, then we will need to use a conditional statement. If we have a nested data structure that we need to iterate over, we will need to use a nested loop. Likewise, if we need to compare two values, we'll need to use a some type of operator (i.e. comparison, logical, identity, etc.). Knowing how and when to use these tools will greatly reduce the amount of code we write as well as greatly increase the efficiency of the code we write.
