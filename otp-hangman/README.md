# Hangman—The OTP iteration

It's time to take our Hangman game up a notch.

This assignment takes Hangman and turns it into a supervised set of OTP servers.

We'll be taking two modules, Game and Dictionary, and making servers of each.

These modules will be part of a supervision tree. The constraints of
this supervision are simple:

If the Game exits normally, do nothing. If it crashes, restart it (and just it).

If the Dictionary exits for any reason, kill any game, and restart both the
Dictionary and the Game.


Converted the current dictionary module to a GenServer inline (that is, the
dictionary code and the GenServer api and callbacks will all be in the
dictionary module).

Registered the dictionary server under the name `:dictionary`.

Converted the game to a GenServer using the *outside* style

added top-level supervision to `lib/hangman.ex`, and
added a second subsupervisor in `lib/hangman/...`.

Updated `mix.exs` to start the servers automatically (by
referencing the top-level supervisor).


You'll play the game using

~~~ elixir
status = Hangman.GameServer.make_move(guess)
~~~

Where status is one of `:won`, `:lost`, `:good_guess`, or `:bad_guess`.

The other API calls are

~~~
length       = Hangman.GameServer.word_length
letters_used = Hangman.GameServer.letters_used_so_far
turns_left   = Hangman.GameServer.turns_left
word         = Hangman.GameServer.word_as_string(reveal = true|false)
~~~




