# TouchDesigner Facebook Help Group and Forum Files
## Programmer / Artist ##
**Matthew Ragan** | [ matthewragan.com](http://matthewragan.com)  

## Contents and Descriptions ##

### base_animation_different_duration ###


### base_animation_offset ###


### base_audio_reactive_revolve ###


### base_blob_track ###


### base_chop_math ###


### base_circles_and_graphs ###


### base_connect_example ###


### base_cooking_example ###


### base_countdown ###


### base_crop_text ###


### base_dispaly_fx ###


### base_drawing_cirlces ###


### base_every_2_minutes ###


### base_movie_player_with_extensions ###


### base_multi_module_config ###


### base_multi_output_config ###


### base_panel_execute ###


### base_particle_alpha_by_life ###


### base_particles_instance_force ###


### base_play_only_if_complete ###


### base_rotate_to_vector ###


### base_row_addition ###


### base_scalex_scaley ###


### base_setting_channels ###


### base_setting_resolution ###


### base_shuffle_chop ###


### base_stop_cooking ###


### base_switch_TOP ###


### base_text_arrangement ###


### base_trigger_only_when_3 ###


### base_two_colors_for_text ###


### base_two_panel_sync ###


### base_wire_fx_techniques ###


### container_blend_chop ###


### container_camera_animation ###


### container_camera_blend_comp ###


### container_channel_mask_via_osc ###


### container_childers_bin_and_display ###


### container_display_breakup ###


### container_drag_drop_container_get_path ###
_**5.19.16**_

**Original post / question**

>Another drag&drop question.
How do I drop a component onto another component, but not actually drop anything, only access the arguments. Essentially I just need the path of a child of the dragged component and use it in a drop script of the receiving component, without actually dropping the component itself. I find the drag and drop wiki page quite confusing.
>

All of the interesting stuff here is really happening in the drag/ drop script that's inside of container_drop.

Here the script is appending a text dat with information from the args that come from a drag / drop event.

The important consideration here is to make sure the replicants are set-up to be drag-drop ready. In our case that means that the replicated containers in container_drag. We want these to have their drag parameter set up correctly so that we can see args associated with them correctly display.

If you're curious to see all of the args associated with this kind of event you might uncomment the for loop at the top of the script and open the text port. Now you can see each of the args printed on its own line. 

### container_draw_path ###


### container_image_per_face ###


### container_instance_resize ###


### container_instance_rot ###

 
### container_instances_rotate_to_vector ###

 
### container_layout ###

 
### container_letter_particles ###

 
### container_live_draw ###

 
### container_manual_and_pattern_instancing ###

 
### container_moving_points ###


### container_object_tracer ###

 
### container_particles ###

 
### container_persistent_slider_vals ###

 
### container_presets_dict_method ###


### container_presets_table_method ###
 

### container_renderpick_drop ###

_**5.8.16**_

**Original post / question**

>Has anyone managed to make a drop script using renderpick? I'm trying to drop movie files onto rendered geometry ut renderpick stops working when you are "holding" a file from the os, even when strategy = always. I've tried using sleep() ut I can't get it.
>

### container_selects_to_stop_cooking ###
 

### container_simple_instance ###
 

### container_single_camera_along_path ###


### container_spiralgraph ###


### container_text_scroll_widths ###

 
### container_texture_sop_perspective_of_camera ###

 
### container_tiled_images ###

 
### container_using_selects ###


### container_xml_example ###
_**4.6.16**_

My suffering is your gain...
Here you'll find a simplified implementation of building out a multi-machine configuration file as XML or JSON. A list comp allows the user to add machines to you heart's content. Double click list comp fields to edit the machine name, edit the text fields to change attributes. Output either XML or JSON.
Some Highlights:
* uses extensions
* uses new global op shortcuts
* uses the list comp with custom parameters
* uses storage to transport all of the relevant data
* uses some fun dictionary loops
* uses doc strings for self documenting methods

### slider_mike ###
_**5.6.16**_

**Original post / question**

>Hi guys, I've got a chop that I want to show some number between 0 and 20. I have an increment value running to a speed chop into a null for that value. I want to have a button to stop incrementing it, (which is a multiply value in a math chop). I want a slider to continually be updated to show that chop value, but when I stop having it autoincrement, I want the slider to be able to control the chop value. Any suggestions?
>

### base_simple_motion_blur ###
_**5.20.16**_

A fast look at how to set-up motion blur.

### base_cell_contents ###
_**5.22.16**_

Original post / question:

>Here is what i want to do and am a little lost.
i have text in lets say the 0,0 cell in table one and a blank space in cell 0,3 in table 2
is there a command i can write to take the text in table 1 cut it and paste it in the feild in table 2. 
id like to do this with a interface so you select name one and it pastes in to slot 2.
>

In this example we have a table, and we want to copy the contents from one place in the table into another table.

For the sake of simplicity let's start with assuming that we're always copying to the same location.

Here we write a simple helper function that's an abstract form of what we're after:

```Python
target = op( 'table_target' )
source = op( 'table_source' )

def Copy_to_target( source_row, _source_col ):

    target[ 0, 0 ] = source[ source_row, _source_col ]

    return

```

Our helper fucntion takes a coordinate location in the table, and copies to the coordinate [ 0, 0] in our target table. 

Rather than write this as a single sciprt, we can instead use it as a module so we can call this action from multiple locations.

```Python
mod( 'text_copy_paste_script' ).Copy_to_target( 3, 3 )
```

Right click and run either text_example1 or text_example2 to see it in action.

### base_one_line_conditional_expressions ###
_**5.22.16**_

Conditional one line Python expressions can be used for a number of different applications.

Let's imagine a circumstance where we have two different sets of animation data. Depending on another variable we want to select the appropriate set of channels. 

In this example, both base comps are identical with one exception, the store key "animation_index".

In base_exampel1 animation_index is set to 0, while in base_example2 animation_index is set to 1. 

Let's take a closer look at our select CHOPs inside of our base components. Here we see a select with the following expression:

```Python
me.fetch( 'animation1' ) if me.fetch( 'animation_index' ) == 0 else me.fetch( 'animation2' )
```

We can pull apart the structure of this a little to better understand what's going on:

[ if_value ] [ logical_test ] [ else_value ]

Seen this way, we can see that the above single line expression looks something like this in plain English:

select op( 'null1' ) if the animation_index value is exactly 0, otherwise select op( 'null2' )

Let's look quickly at another example. In table1 we have two rows. The eval DATs below have the following expression:

```Python
op( 'table1' )[ 0, 0 ] if me.digits == 1 else op( 'table1' )[ 1, 0 ]
```

So here we can see that we select the cell in the [ 0, 0 ] position if our digits are 1, in all other cases we select the cell in the [ 1, 0 ] position.

### base_change_comp_top ###
_**5.24.16**_

**Original post / question**

>Quick question... I am using a composite top and would like to be able to select the operation type in perform mode, however, how can I connect the comp operation to a list so that the names of the operations (divide, dodge, burn etc) are shown in the list. I have got as far as using a parameter chop to fetch the operator number but not the name. ideally would like to have a list of names I can select from.
Does this make sense?
From the looks of the example, its necessary to add in the individual operation names into table2 manually, is there not a way of capturing those names from the comp? or am I missing something.?
>

Some parameters are accessible as lists, this is often the case when thinking about the parameters that have drop down menus. Items in the drop down have a position in a list that corresponds to a value. We can do all sorts of things to change these parameters, and in the case of the composite TOP we can set the blending operation mode with something like:

```Python
op( 'comp1' ).par.operand = 0
```

That's the root of the challenge. If we want a UI element that set that parameter when we click a corresponding label we need to know the index of the label so we can create a relationship between these two.

If we have a table COMP we can do something like this with a panel execute:

```Python
op( '../comp1' ).par.operand = parent().panel.celloverid
```

"But Matt!" You'll cry out.
"I don't want to go through and make a list of all of the elements in a given parameter. Isn't there a better way?!"

Sure.

```Pytyhon
op( 'comp1' ).par.operand.menuNames
```

Will produce a list of menu names, then we need to convert that into a table, then we need to transpose that into rows instead of columns, finally we can then we can feed that into the table COMP.

### base_resample_test ###
_**6.2.16**_

**Original post / question**

>Hey guys, I wanted to ask you for a while now how are you handling this issue: in some circumstances, when converting channels to samples Shuffle Chop it looks a running timeline even though the chop is 1 sample (like LFO). The only time it's actually working for me is converting constant Chop. I tried just swapping or sequencing technique, nothing helps. The only workaroung appears to have a Stretch chop inserted somewhere to "stabilize" the output length. Any ideas? Thx
EDIT: forgot to tell that I'm using the option "Use First Sample Only" in Shuffle. Build 60230
>

Suggestions came in to try the stretch, resample, stretch, or trim CHOPs as possible solutions to this problem. The question then is, which is the fastest?

*Cook times at a Glance*

| CHOP      | Cook Time in Milliseconds    |
|-----------|------------------------------|
| Resample  | 0.0143                       |
| Trim      | 0.0049                       |
| Stretch   | 0.0045                       |
| Shift     | 0.0041                       |

*Max Cook times over 10 Seconds*

| CHOP      | Cook Time in Milliseconds    |
|-----------|------------------------------|
| Resample  | 0.0616                       |
| Trim      | 0.1191                       |
| Stretch   | 0.0374                       |
| Shift     | 0.0246                       |

*Average Cook times over 10 Seconds*

| CHOP      | Cook Time in Milliseconds    |
|-----------|------------------------------|
| Resample  | 0.0179                       |
| Trim      | 0.0062                       |
| Stretch   | 0.0081                       |
| Shift     | 0.0059                       |

I think I'd go with averge cook time as a benchmark, given that this is probably used over time. With that in mind, it looks like it's a tie between trim and shift.

### base_instancing_instances ###
_**6.2.16**_

**Original post / question**

>Hello group! Is it possible to instance a geo containing an instanced geo? Maybe I'm doing something wrong here but it doesn't seem to be! Is there one of those ''obvious once you know it'' answers to why this is?
Pretty sure instancing is limited to one layer. (I'd love to be proven wrong). You can do this behaviour in Houdini with packed primitives.
From what I see it doesn't seem to be possible. I can get to the same result by making a more complex network feeding the first set of instances but it's not as tidy as it would be otherwise know what I mean?
>

instancing instances is just about doing the math in CHOPs to determine the location of the instances.

Two Examples

* instance a copy sop - this is the effect we want
* chop math for the same effect - this is how to get there with just instances and CHOP math

All that CHOP data is just the location for copies to be drawn by the GPU. 

In the second example: 
* I use the box to find the coordinates for our corners
* shuffle that to expose all of the coordinates. * Next add the second set of locations
* then shuffle again to end up with a single set of xyz coordinates for the instances.

### base_input_replication ###
_**6.8.16**_

**Original post / question**

>Any way to create in multi-in for an container like, for example, in the composite top?
there isn't a multi in the same way you see in the multi in TOPs. You can, however, use a Composite TOP, which now has a selection field where you can add any number of operators
Good to know, but sadly this is not what i am looking in to. The idear is to create an video-mixer wich automatcly creates ne sliders for every new input. I tried to monitor the number of inputs and at a change create a new in-top. The value changes inside the value0-param but it does not seem to update the channel itself wich i need to fire my script.
>

Actually we can generate a list of inputs with just a little bit of clever Python.

First we need to grab the string that's in the top parameter field in our composite TOP. We can do this with the following expression:

```Python
op( 'comp1' ).par.top.val
```

Next we'll convert this into a set of rows, transpose this so we have columns, and then we have something we can use to drive a replicator in order to create sliders on the fly.

### container_slider_jonas ###
_**6.14.16**_

**Original post / question**

>Having trouble with sliders. By now i can use them pretty fine, but only when I use them alone. When i put more then one inside of an container the problems occur. I tried playing arround with different par (clicktrhough, enable, visible, layer). attached an trying tox to understand what i want to archive. Maybe someone can give me a hint.
>

Rather than using two sliders and trying to toggle their click-through on and off, we might be better off to build our own. Sliders, after all, are just containers with a knob that report out a normalized value. 

Starting with this simple two knob concept we can quickly see how we might scale up to an even larger number of knobs in the future. The big idea here is to think of writing the insideu value of our parent container into a constant, which is then used to determine the x coordinate of the knob. 

We also want to build this smartly so it only cooks when we're actually interacting with this element. That may seem obvious, but it can be a tricky undertaking in touch. 