## willevlab SDL3 Sokoban

Hold 'Space' and move directly away from the BigCheese™ to pull it with you.

Mousetrap is the Sokoban-style puzzle game I made in six weeks for my C++ course at Yrgo, Sweden. You play a mouse who pushes and pulls blocks, eats all the cheese in the level and then makes it to the purple portal. It is written in C++20 for Windows, built with CMake, Ninja and clang++. There is no game engine underneath it. SDL3 handles the window, input, and drawing, and mostly everything else is written specifically for this game, apart from the material given to me by my teacher. The logic lives in a DLL that a small host program loads, and when the DLL is rebuilt the host swaps it in while the game keeps running, so code changes show up without a restart. F9 saves the whole game state and F10 restores it, which made it really easy to playtest in the earlier drafts of this project. All memory is allocated up front as one 10 MB block and split into arenas for images, levels, entities, undo commands, input, UI, and audio.

I drew the levels in Tiled and exported them as JSON, which the game reads with nlohmann/json, from GitHub. Each level has a tile layer and an entities layer for the player, the blocks and items like cheese. The tileset marks which tiles are walkable with a `walkable` property. The menu is built to be easy to use with whatever a player happens to be holding. It works with only the keyboard or only the mouse, and neither needs the other. Menus like these are very important to me and also very fun to create.

The tunnels were the hardest part to get working. A mouse hole leads into a level nested inside another level, in chains of up to three, and the undo history, moving between levels, and checking whether a level is complete all have to work across the whole chain. The tunnel levels are also what I am proudest of over course of this development. Making Mousetrap taught me about managing memory, structuring a bigger C++ project and using tools like CMake, Tiled, and hot reloading.

Sound is played through FMOD. The music and sound effects were purely made by AI; generated with Python scripts (numpy) instead of being recorded or downloaded. I had always wanted to test just that, and it sounds pretty alright I guess.

I used [SDL3](https://libsdl.org), SDL3_image and SDL3_ttf (zlib license), [FMOD](https://www.fmod.com) by Firelight Technologies Pty Ltd for audio playback, [Dear ImGui](https://github.com/ocornut/imgui) by Omar Cornut and [nlohmann/json](https://github.com/nlohmann/json) by Niels Lohmann (both MIT license), and [Tiled](https://www.mapeditor.org) for the levels. I set the text in the Press Start 2P font by The Press Start 2P Project Authors under the SIL Open Font License 1.1, and the license text is in `assets/fonts/PressStart2P-OFL.txt`.

Thanks for checking out Mousetrap!

This is also the first time I've created an entire tileset myself
