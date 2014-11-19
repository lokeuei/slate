## Errors

<h2>Message</h2>

<p>Generic format for error messages in output objects. Errors are returned in the Message class. <a href="http://developer.avalara.com/api-docs/designing-your-integration/errors-and-outages/common-errors">See Error Lists</a>.</p>

<h2>Properties</h2>

<p><strong>Summary:</strong> string [int MAX_VALUE]</p>

<p>The message summary in short form.</p>

<p><strong>Details:</strong> string [int MAX_VALUE]</p>

<p>Description of the error or warning.</p>

<p><strong>RefersTo:</strong> string [int MAX_VALUE]</p>

<p>The data used during the request that caused the message to be generated.</p>

<p><strong>Severity:</strong> enum as string [see below]</p>

<p>Classifies severity of message. One of:</p>

<ul class="task-list">
<li>Success</li>
<li>Error</li>
<li>Warning</li>
<li>Exception</li>
</ul><p><strong>Source:</strong> string [int MAX_VALUE]</p>

<p>The internal location that generated the message.</p>