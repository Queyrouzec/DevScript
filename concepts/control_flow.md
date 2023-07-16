# Control Flow

Control flow in js is made up of if, else, for, functions, maybe switch statements, and occasionally a weird looking object thing. This is pretty limited for something that is so core to building dynamic programs.

## Goals of Extra Control Flow methods

- should increase brevity
- should declare it's intent as early as possible
- should limit the variables and ideas you have to keep in mind
- compilation should be clear, predictable, and avoid extra closers.

## Elixir

Of the languages I've used, Elixir has the best control flow. Rust has many of it's control flow methods and will hopefully have many more, but as of right now it's lacking in many key flow optimizations.

Let's one of the ways you can avoid nested or excessive if statements in Elixir.

```elixir
# in elixir a colon followed by a text is a way of saying this is a string significant to developers.
def get_expected_internet_speed(user_id) do
    with %{zip_code: zip_code} <- get_user(id: user_id),
        # must match previous statement to run this statement, otherwise it'll move to the else block.
        # can use zip_code from the previous statement
        %{average_user_speed: average_user_speed} <- get_internet_statistics(zip_code) do
        # runs this if everything matches
        print(average_user_speed) # 250 mbps
    else
        # if the statements don't match it'll try to match one of these statements
        {:error, :user_does_not_exist} -> print("user does not exist")
        {:error, :no_data_on_area} -> print("area does not have internet statistics")
        # This matches everything. It is how you provide a default statement. If this didn't exist and nothing matched it'd return the unmatched values.
        error -> print(error)
    end
end
# or without comments
def get_expected_internet_speed(user_id) do
    with %{zip_code: zip_code} <- get_user(id: user_id),
          %{average_user_speed: average_user_speed} <- get_internet_statistics(zip_code) do
        print(average_user_speed)
    else
        {:error, :user_does_not_exist} -> print("user does not exist")
        {:error, :no_data_on_area} -> print("area does not have internet statistics")
        error -> print(error)
    end
end
```

vs the js equivalent

```javascript
function getExpectedInternetSpeed(user_id) {
  let user = ({ zipCode, error } = getUser(user_id));
  if (zipCode != undefined) {
    let internetStatistics = ({ averageUserSpeed, error } =
      getInternetStatistics(zipCode));
    if (averageUserSpeed != undefined) {
      print(averageUserSpeed);
    } else if (error == "no_data_on_area") {
      print("area does not have internet statistics");
    } else {
      print(internetStatistics);
    }
  } else if (error == "user_does_not_exist") {
    print("user does not exist");
  } else {
    print(user);
  }
}
```

The Elixir's `with` statements ability to run one condition after another is extremely powerful.

- It creates a clear process of events
- It limits the scope under which you must keep variable declarations in mind
- It allows for clearer destructuring and eliminates the need for a user and internetStatistics object
- It makes multiple types of returns more easily useable and in turn creates a clearer error handling paradigm
