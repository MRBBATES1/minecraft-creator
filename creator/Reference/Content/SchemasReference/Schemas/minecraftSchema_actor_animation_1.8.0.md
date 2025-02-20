---
author: v-jeffreykim
ms.author: v-jeffreykim
title: "Schema Documentation - actor_animation:1.8.0"
ms.prod: gaming
---

# Schema Documentation - actor_animation:1.8.0

This schema corresponds to the *.animation.json files in the "animations" folder of the resource pack.

```json
actor_animation:1.8.0:{
    version "format_version"
    object "animations"
    {
        object "animation.<identifier>"
        {
            bool "loop" : opt // should this animation stop, loop, or stay on the last frame when finished (true, false, "hold_on_last_frame")
            string "loop"<"hold_on_last_frame"> : opt // should this animation stop, loop, or stay on the last frame when finished (true, false, "hold_on_last_frame")
            molang "start_delay" : opt // How long to wait in seconds before playing this animation.  Note that this expression is evaluated once before playing, and only re-evaluated if asked to play from the beginning again.  A looping animation should use 'loop_delay' if it wants a delay between loops.
            molang "loop_delay" : opt // How long to wait in seconds before looping this animation.  Note that this expression is evaluated after each loop and on looping animation only.
            molang "anim_time_update" : opt // how does time pass when playing the animation.  Defaults to "query.anim_time + query.delta_time" which means advance in seconds.
            molang "blend_weight" : opt
            bool "override_previous_animation" : opt // reset bones in this animation to the default pose before applying this animation
            object "bones" : opt
            {
                object "<identifier>"
                {
                    object "relative_to" : opt
                    {
                        string "rotation"<"entity"> : opt // if set, makes the bone rotation relative to the entity instead of the bone's parent
                    }
                    molang "position" : opt
                    object "position" : opt
                    {
                        object "<time_stamp>"
                        {
                            enumerated_value "lerp_mode"<"linear", "catmullrom"> : opt
                            array "pre"[3] : opt
                            {
                                molang "<any array element>"
                            }
                            array "post"[3] : opt
                            {
                                molang "<any array element>"
                            }
                        }
                        array "<time_stamp>"[3]
                        {
                            molang "<any array element>"
                        }
                    }
                    array "position" : opt
                    {
                        molang "<any array element>"
                    }
                    molang "rotation" : opt
                    array "rotation" : opt
                    {
                        molang "<any array element>"
                        object "<any array element>"
                        {
                            molang "[xyz]"
                        }
                    }
                    object "rotation" : opt
                    {
                        object "<time_stamp>"
                        {
                            enumerated_value "lerp_mode"<"linear", "catmullrom"> : opt
                            array "pre"[3] : opt
                            {
                                molang "<any array element>"
                            }
                            array "post"[3] : opt
                            {
                                molang "<any array element>"
                            }
                        }
                        array "<time_stamp>"[3]
                        {
                            molang "<any array element>"
                        }
                    }
                    molang "scale" : opt
                    object "scale" : opt
                    {
                        object "<time_stamp>"
                        {
                            enumerated_value "lerp_mode"<"linear", "catmullrom"> : opt
                            array "pre"[3] : opt
                            {
                                molang "<any array element>"
                            }
                            array "post"[3] : opt
                            {
                                molang "<any array element>"
                            }
                        }
                        array "<time_stamp>"[3]
                        {
                            molang "<any array element>"
                        }
                    }
                    array "scale" : opt
                    {
                        molang "<any array element>"
                    }
                }
            }
            object "particle_effects" : opt
            {
                array "<time_stamp>" : opt
                {
                    object "<any array element>" : opt
                    {
                        string "effect" // The name of a particle effect that should be played
                        string "locator" : opt // The name of a locator on the actor where the effect should be located
                        molang "pre_effect_script" : opt // A molang script that will be run when the particle emitter is initialized
                        bool "bind_to_actor" : opt // Set to false to have the effect spawned in the world without being bound to an actor (by default an effect is bound to the actor).
                    }
                }
                object "<time_stamp>" : opt
                {
                    string "effect" // The name of a particle effect that should be played
                    string "locator" : opt // The name of a locator on the actor where the effect should be located
                    molang "pre_effect_script" : opt // A molang script that will be run when the particle emitter is initialized
                    bool "bind_to_actor" : opt // Set to false to have the effect spawned in the world without being bound to an actor (by default an effect is bound to the actor).
                }
            }
            object "sound_effects" : opt // sound effects to trigger as this animation plays, keyed by time
            {
                array "<time_stamp>" : opt
                {
                    object "<any array element>" : opt
                    {
                        string "effect" // Valid sound effect names should be listed in the entity's resource_definition json file.
                    }
                }
                object "<time_stamp>" : opt
                {
                    string "effect" // Valid sound effect names should be listed in the entity's resource_definition json file.
                }
            }
            object "timeline" : opt
            {
                string "<time_stamp>" : opt
                array "<time_stamp>" : opt
                {
                    string "<any array element>" : opt
                }
            }
            float "animation_length" : opt // override calculated value (set as the last keyframe time) and set animation length in seconds.
        }
    }
}
```