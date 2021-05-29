# Plugins

In jsPsych, plugins define the kinds of tasks that subjects perform in experiments. Some plugins define very general tasks, like displaying instructions or displaying a visual stimulus and getting a keyboard response. Other plugins are more specific, displaying particular kinds of interactive stimuli, or running a specific version of particular kind of task. Creating an experiment with jsPsych involves figuring out which plugins are needed for the kinds of tasks you want to have your subjects perform.

Plugins provide a structure for a particular task, but often allow for significant customization and flexibility. For example, the `jspsych-image-keyboard-response` plugin defines a simple structure for showing an image and collecting a keyboard response. You can specify the what the stimulus is, what keys the subject is allowed to press, and how long the stimulus should be on the screen, how long the subject has to respond, and so on. Many of these content options have reasonable default values; even though the `jspsych-image-keyboard-response` plugin has many different options, you only *need* to specify the stimulus in order to use it. Each plugin has its own documentation page, which describes what the plugin does and what options are available.

## Using a plugin

To use a plugin, you'll need to load the plugin's JavaScript file on your experiment page:

```html
<head>
<script src="jspsych/plugins/jspsych-image-keyboard-response.js" type="text/javascript"></script>
</head>
```

Once a plugin is loaded, you can define a trial that uses that plugin. The following JavaScript code defines a trial using the `jspsych-image-keyboard-response` plugin to display an image file ('images/happy_face.jpg'). This trial uses the default values for valid keys, length of display, and other parameters. You could override these values by adding them to the object.

```javascript
var single_stim_trial = {
	type: 'image-keyboard-response',
	stimulus: 'images/happy_face.jpg'
}
```

Here's an exampe of overriding the default value for `post_trial_gap`:

```javascript
var single_stim_trial = {
	type: 'image-keyboard-response',
	stimulus: 'images/happy_face.jpg',
	post_trial_gap: 2000
}
```

## Parameters available in all plugins

Each plugin specifies its own set of parameters. Check the documentation for a plugin to see what parameters are available and what they do.

In addition, there is a set of parameters that can be specified for any plugin.

Parameter | Type | Default Value | Description
----------|------|---------------|------------
post_trial_gap | numeric | null | Sets the time, in milliseconds, between the current trial and the next trial. If null, there will be no gap.
on_finish | function | `function(){ return; }` | A callback function to execute when the trial finishes. See [this page](../overview/callbacks.md) for more details.
on_start | function | `function(){ return; }` | A callback function to execute when the trial begins, before any loading has occurred. See [this page](../overview/callbacks.md) for more details.
on_load | function | `function(){ return; }` | A callback function to execute when the trial has loaded, which typically happens after the initial display of the plugin has loaded. See [this page](../overview/callbacks.md) for more details.
data | object | *undefined* | An object containing additional data to store for the trial. See [this page](../overview/data.md) for more details.
css_classes | string | null | A list of CSS classes to add to the jsPsych display element for the duration of this trial. This allows you to create custom formatting rules (CSS classes) that are only applied to specific trials. See jsPsych/examples/css-classes-parameter.html for examples.

## Data collected by plugins

Each plugin defines what data is collected on the trial. The documentation for each plugin specifies what data is collected by that plugin.

In addition to the data collected by a plugin, there is a default set of data that is collected on every trial. The collected data are:

Name | Type | Value
-----|------|------
trial_type | string | The name of the plugin used to run the trial.
trial_index | numeric | The index of the current trial across the whole experiment.
time_elapsed | numeric | The number of milliseconds since the start of the experiment when the trial ended.
internal_node_id | string | A string identifier for the current TimelineNode.

## List of available plugins

This table is a description of all plugins that are distributed with jsPsych. Click on the name of a plugin to view its documentation page.

Plugin | Description
------ | -----------
[jspsych&#8209;animation](/plugins/jspsych-animation) | Shows a sequence of images at a specified frame rate. Records key presses (including timing information) made by the subject while they are viewing the animation.
[jspsych&#8209;audio&#8209;button&#8209;response](/plugins/jspsych-audio-button-response) | Play an audio file and allow the subject to respond by choosing a button to click. The button can be customized extensively, e.g., using images in place of standard buttons.
[jspsych&#8209;audio&#8209;keyboard&#8209;response](/plugins/jspsych-audio-keyboard-response) | Play an audio file and allow the subject to respond by pressing a key.
[jspsych&#8209;audio&#8209;slider&#8209;response](/plugins/jspsych-audio-slider-response) | Play an audio file and allow the subject to respond by moving a slider to indicate a value.
[jspsych&#8209;call&#8209;function](/plugins/jspsych-call-function) | Executes an arbitrary function call. Doesn't display anything to the subject, and the subject is usually unaware that this plugin has even executed. It's useful for performing tasks at specified times in the experiment, such as saving data.
[jspsych&#8209;canvas&#8209;button&#8209;response](/plugins/jspsych-canvas-button-response) | Draw a stimulus on a [HTML canvas element](https://www.w3schools.com/html/html5_canvas.asp), and record a button click response. Useful for displaying dynamic, parametrically-defined graphics, and for controlling the positioning of multiple graphical elements (shapes, text, images).
[jspsych&#8209;canvas&#8209;keyboard&#8209;response](/plugins/jspsych-canvas-keyboard-response) | Draw a stimulus on a [HTML canvas element](https://www.w3schools.com/html/html5_canvas.asp), and record a key press response. Useful for displaying dynamic, parametrically-defined graphics, and for controlling the positioning of multiple graphical elements (shapes, text, images).
[jspsych&#8209;canvas&#8209;slider&#8209;response](/plugins/jspsych-canvas-slider-response) | Draw a stimulus on a [HTML canvas element](https://www.w3schools.com/html/html5_canvas.asp), and ask the subject to respond by moving a slider to indicate a value. Useful for displaying dynamic, parametrically-defined graphics, and for controlling the positioning of multiple graphical elements (shapes, text, images).
[jspsych&#8209;categorize&#8209;animation](/plugins/jspsych-categorize-animation) | The subject responds to an animation and can be given feedback about their response.
[jspsych&#8209;categorize&#8209;html](/plugins/jspsych-categorize-html) | The subject responds to an HTML-formatted stimulus using the keyboard and can be given feedback about the correctness of their response.
[jspsych&#8209;categorize&#8209;image](/plugins/jspsych-categorize-image) | The subject responds to an image using the keyboard and can be given feedback about the correctness of their response.
[jspsych&#8209;cloze](/plugins/jspsych-cloze) | Plugin for displaying a cloze test and checking participants answers against a correct solution.
[jspsych&#8209;external&#8209;html](/plugins/jspsych-external-html) | Displays an external HTML page (such as a consent form) and lets the subject respond by clicking a button or pressing a key. Plugin can validate their response, which is useful for making sure that a subject has granted consent before starting the experiment.
[jspsych&#8209;free&#8209;sort](/plugins/jspsych-free-sort) | Displays a set of images on the screen in random locations. Subjects can click and drag the images to move them around the screen. Records all the moves made by the subject, so the sequence of moves can be recovered from the data.
[jspsych&#8209;fullscreen](/plugins/jspsych-fullscreen) | Toggles the experiment in and out of fullscreen mode.
[jspsych&#8209;html&#8209;button&#8209;response](/plugins/jspsych-html-button-response) | Display an HTML-formatted stimulus and allow the subject to respond by choosing a button to click. The button can be customized extensively, e.g., using images in place of standard buttons.
[jspsych&#8209;html&#8209;keyboard&#8209;response](/plugins/jspsych-html-keyboard-response) | Display an HTML-formatted stimulus and allow the subject to respond by pressing a key.
[jspsych&#8209;html&#8209;slider&#8209;response](/plugins/jspsych-html-slider-response) | Display an HTML-formatted stimulus and allow the subject to respond by moving a slider to indicate a value.
[jspsych&#8209;iat&#8209;html](/plugins/jspsych-iat-html) | The implicit association task, using HTML-formatted stimuli.
[jspsych&#8209;iat&#8209;image](/plugins/jspsych-iat-image) | The implicit association task, using images as stimuli.
[jspsych&#8209;image&#8209;button&#8209;response](/plugins/jspsych-image-button-response) | Display an image and allow the subject to respond by choosing a button to click. The button can be customized extensively, e.g., using images in place of standard buttons.
[jspsych&#8209;image&#8209;keyboard&#8209;response](/plugins/jspsych-image-keyboard-response) | Display an image and allow the subject to respond by pressing a key.
[jspsych&#8209;image&#8209;slider&#8209;response](/plugins/jspsych-image-slider-response) | Display an image and allow the subject to respond by moving a slider to indicate a value.
[jspsych&#8209;instructions](/plugins/jspsych-instructions) | For displaying instructions to the subject. Allows the subject to navigate between pages of instructions using keys or buttons.
[jspsych&#8209;maxdiff](/plugins/jspsych-maxdiff) | Displays rows of alternatives to be selected for two mutually-exclusive categories, typically as 'most' or 'least' on a particular criteria (e.g. importance, preference, similarity). The participant responds by selecting one radio button corresponding to an alternative in both the left and right response columns.
[jspsych&#8209;rdk](/plugins/jspsych-rdk) | This plugin displays a Random Dot Kinematogram (RDK) and allows the subject to report the primary direction of motion by pressing a key on the keyboard.
[jspsych&#8209;reconstruction](/plugins/jspsych-reconstruction) | The subject interacts with a stimulus by modifying a parameter of the stimulus and observing the change in the stimulus in real-time.
[jspsych&#8209;resize](/plugins/jspsych-resize) | Calibrate the display so that materials display with a known physical size.
[jspsych&#8209;same&#8209;different&#8209;html](/plugins/jspsych-same-different-html) | A same-different judgment task. An HTML-formatted stimulus is shown, followed by a brief gap, and then another stimulus is shown. The subject indicates whether the stimuli are the same or different.
[jspsych&#8209;same&#8209;different&#8209;image](/plugins/jspsych-same-different-image) | A same-different judgment task. An image is shown, followed by a brief gap, and then another stimulus is shown. The subject indicates whether the stimuli are the same or different.
[jspsych&#8209;serial&#8209;reaction&#8209;time](/plugins/jspsych-serial-reaction-time) | A set of boxes are displayed on the screen and one of them changes color. The subject presses a key that corresponds to the different color box as fast as possible.
[jspsych&#8209;serial&#8209;reaction&#8209;time&#8209;mouse](/plugins/jspsych-serial-reaction-time-mouse) | A set of boxes are displayed on the screen and one of them changes color. The subjects clicks the box that changed color as fast as possible.
[jspsych&#8209;survey&#8209;html&#8209;form](/plugins/jspsych-survey-html-form) | Renders a custom HTML form. Allows for mixing multiple kinds of form input.
[jspsych&#8209;survey&#8209;likert](/plugins/jspsych-survey-likert) | Displays likert-style questions.
[jspsych&#8209;survey&#8209;multi&#8209;choice](/plugins/jspsych-survey-multi-choice) | Displays multiple choice questions with one answer allowed per question.
[jspsych&#8209;survey&#8209;multi&#8209;select](/plugins/jspsych-survey-multi-select) | Displays multiple choice questions with multiple answes allowed per question.
[jspsych&#8209;survey&#8209;text](/plugins/jspsych-survey-text) | Shows a prompt with a text box. The subject writes a response and then submits by clicking a button.
[jspsych&#8209;video&#8209;button&#8209;response](/plugins/jspsych-video-button-response) | Displays a video file with many options for customizing playback. Subject responds to the video by pressing a button.
[jspsych&#8209;video&#8209;keyboard&#8209;response](/plugins/jspsych-video-keyboard-response) | Displays a video file with many options for customizing playback. Subject responds to the video by pressing a key.
[jspsych&#8209;video&#8209;slider&#8209;response](/plugins/jspsych-video-slider-response) | Displays a video file with many options for customizing playback. Subject responds to the video by moving a slider.
[jspsych&#8209;visual&#8209;search&#8209;circle](/plugins/jspsych-visual-search-circle) | A customizable visual-search task modelled after [Wang, Cavanagh, & Green (1994)](http://dx.doi.org/10.3758/BF03206946). The subject indicates whether or not a target is present among a set of distractors. The stimuli are displayed in a circle, evenly-spaced, equidistant from a fixation point.
[jspsych&#8209;vsl&#8209;animate&#8209;occlusion](/plugins/jspsych-vsl-animate-occlusion) | A visual statistical learning paradigm based on [Fiser & Aslin (2002)](http://dx.doi.org/10.1037//0278-7393.28.3.458). A sequence of stimuli are shown in an oscillatory motion. An occluding rectangle is in the center of the display, and the stimuli change when they are behind the rectangle.
[jspsych&#8209;vsl&#8209;grid&#8209;scene](/plugins/jspsych-vsl-grid-scene) | A visual statistical learning paradigm based on [Fiser & Aslin (2001)](http://dx.doi.org/10.1111/1467-9280.00392). A scene made up of individual stimuli arranged in a grid is shown. This plugin can also generate the HTML code to render the stimuli for use in other plugins.
