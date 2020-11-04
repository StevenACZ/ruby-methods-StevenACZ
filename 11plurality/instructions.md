# Plurality

> Thanks again to CS50 for the inspiration 🙂

The program should works as follow:

```
$ ruby plurality.rb
Candidates names: Diego Wences Deyvi
Number of voters: 5
--------------------
Voter 1: Wences
Voter 2: Deyvi
Voter 3: Diego
Voter 4: Diego
Voter 5: Diego
--------------------
Winners: Diego
$
```

> Perhaps the simplest way to hold an election, though, is via a method commonly known as the
> “plurality vote” (also known as “first-past-the-post” or “winner take all”). In the plurality
> vote, every voter gets to vote for one candidate. At the end of the election, whichever candidate
> has the greatest number of votes is declared the winner of the election.
> -CS50

Our version of the Plurality program should:

- Ask the user for the name of the candidates (minimum 1 and maximum 9)
- Then ask for the number of voters (a positive number)
- Then, for each voter, it should ask for the name of the candidate they want to vote and then
  increase the number of votes for that candidate by one.
- After all the voters emmited their votes, the program should print the winner(s)

One part of the program is already written but the methods definitions are missing:

```ruby
# Global variable (do not touch this)
$candidates = []

# Method definitions. To be completed by you:
def get_list(prompt, min, max)
  # to be completed
end

def get_positive(prompt)
  # to be completed
end

def valid_vote?(name)
  # to be completed
end

def print_winner
  # to be completed
end

# The program starts here.
names = get_list("Candidates names: ", 1, 9)

names.each do |name|
  candidate = { "name" => name, "votes" => 0 }
  $candidates.push(candidate)
end

voters_count = get_positive("Number of voters: ")

puts "-" * 20

(1..voters_count).each do |i|
  print "Voter #{i}: "
  name = gets.chomp

  until valid_vote?(name)
    puts "Invalid vote"
    print "Voter #{i}: "
    name = gets.chomp
  end
end

puts "-" * 20

print_winner
```

Your task is to complete the four methods `get_list`, `get_positive`, `valid_vote?` and `print_winner`
following the requirements and passing the tests.

### get_list

- This method ask the user for a list of words separated by a space and return an array whith those
  words as elements.
- This method has 3 parameters:
  - prompt: The message tu display to the user
  - min and max: To validate that the number of words is between these two values.
- If the user input an invalid set of words (an empty string or more than `max` words), then the
  method should display the message `The list should have between <min> and <max> elements` and keep
  asking again.

### get_positive

- This method ask the user for a positive value and return it.
- This method has 1 parameter:
  - prompt: The message tu display to the user
- If the user input an invalid number (negative, zero or letters), then the method should
  display the message `Number should be positive` and keep asking again.

### valid_vote?

- This method receive a name and try to add 1 vote to the corresponding candidate. The
  list of candidates are stored in a `global variable` call `$candidates` (is global only because the
  test needs to access the same variable). Each candidate is stored in a hash with the following form:
  `{ "name" => "candidate_name", "votes" => 0 }`.
- This method has 1 parameter:
  - name: The name of the candidate the user want to vote on.
- If there is a candidate with that name, the method should add 1 to its `votes` property and `return true`
- If the name do not corresponds to any candidate, then the method return `false`

### print_winner

- This method should verify if there is only 1 winner (one candidate with the maximun amount of votes).
- If the are only 1 winner it should display `"Winners: Candidate_name"`
- If there is a tie between 2 or more candidates it should display the name of all of them se parated
  by a comma and a space: `"Winners: Candidate1_name, Candidate2_name"`

## Test

All the test are `skiped` by default. To activate a test just uncommented from the test file

`# skip` -> `skip``

This is for your convinience. If you start working on the `get_list` method just uncomment all the
tests related to that method 🙂

You can even comment al the program code and focus only the methods first. Then uncomment the code
program and run the final test which is oriented to test the program as a whole.

## Examples

Here more examples on how the code should work:

#### Invalid list of candidates

```
$ ruby plurality.rb
Candidates names: a b c d e f g h i j
The list should have between 1 and 9 elements
Candidates names:
The list should have between 1 and 9 elements
Candidates names: 5
Number of voters:
```

(the program continues...)

#### Invalid positive number

```
$ ruby plurality.rb
Candidates names: Diego Deyvi Wences
Number of voters: 0
Number should be positive
Number of voters: -10
Number should be positive
Number of voters: texto
Number should be positive
Number of voters: 5
--------------------
Voter 1:
```

(the program continues...)

#### Invalid candidate name when voting

```
$ ruby plurality.rb
Candidates names: Diego Deyvi Wences
Number of voters: 3
--------------------
Voter 1: Diego
Voter 2: Juan
Invalid vote
Voter 2: Marco
Invalid vote
Voter 2: Wences
Voter 3: Diego
--------------------
Winners: Diego
$
```

#### Tie result

```
$ ruby plurality.rb
Candidates names: Diego Wences Deyvi
Number of voters: 3
--------------------
Voter 1: Wences
Voter 2: Deyvi
Voter 3: Diego
--------------------
Winners: Diego, Wences, Deyvi
$
```
