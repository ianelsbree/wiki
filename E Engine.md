# E Engine

- [E Engine](#e-engine)
  - [Graphics](#graphics)
  - [Audio](#audio)
  - [OS Layer](#os-layer)
  - [Interaction](#interaction)
  - [GUI](#gui)
  - [Other Systems Here](#other-systems-here)

E Engine is a project I'm working on to create my own custom game engine. It's written in Rust.

## Graphics

At this point, I think I'm going to try using [Vulkan](https://www.vulkan.org/), mostly as a learning experience. There's an officially-referenced Rust crate for the Vulkan API called [Ash](https://crates.io/crates/ash) that seems like it might work well. However, the fact that it uses `unsafe` rust bindings has me a little bit worried, so I want to look into what that exactly entails on my end. If that doesn't work out, there's another crate called [Vulkano](https://crates.io/crates/vulkano) that calls itself a safe wrapper, so that would be my other option.

## Audio

I'm likely going with [FMOD](http://studio.fmod.com/) or ~~[Wwise](https://www.audiokinetic.com/en/products/wwise/)~~ for audio as those are the two I'm most familiar with. I have realized that Wwise will likely require a license for the production software, so I will likely be going with FMOD, or possibly something different if I find a different solution.

## OS Layer

I haven't decided on a window framework yet, and my two choices seem to be [GLFW](https://www.glfw.org/) or [SDL2](https://www.libsdl.org/). Might need to look around to see if there are other options for those.

## Interaction

## GUI

I think I want to use either [Dear ImGui](https://github.com/ocornut/imgui) with [imgui-rs](https://crates.io/crates/imgui) or [egui](https://crates.io/crates/egui) for UI elements.

## Other Systems Here

---
Go back to [Projects]  
Created: 2022-11-08  
Last Updated: 2022-11-16  
© 2022 Ian Elsbree  

[Projects]: Projects "Projects"
