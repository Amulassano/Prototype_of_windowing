# Windowing Function
We present a model for analysis called [SECRET](https://people.csail.mit.edu/tatbul/publications/maxstream_vldb10.pdf) that is focussed on time-based windows amd songle-input integer plans.<br>
The windowing function is based on [SECRET](https://people.csail.mit.edu/tatbul/publications/maxstream_vldb10.pdf) Multi-Buffer behaviour, in which the buffer is a list.
## List
### Structure
It's a dynamic list based on nodes. We know the first node that has the first window and the number of nodes in the list.<br> Every nodes is linked to the next time-based node in which the opening and the closure will be older.<br> Moreover a node has the key, that is a window, a content, that is a vector of tuples composed by an element and his timestamp, and the number of contents.
### How does it work?
Every time that the function receives a content it looks for the place where to put it starting by iterating consequentially the list to find the right windows, if it doesn't already exist it will create a new node, linking it with the previous one and eventually with the following one.
## Main components
<ul>
<li>
allocaBuffer(): it allocates the buffer that initially will be empty and the head will be NULL;
</li>
<li>
scope(): it computes the windows and it updates the list creating eventually new windows where to put the content received;
</li>
<li>
addToBuffer(): it adds the content into the list;
</li>
<li>
tick(): it looks if the actual timestamp is older than the previous one;
</li>
<li>
active(): it looks if a window is still activate or not;
</li>
<li>
report(): window_close report;
</li>
<li>
extractData(): it extract a content vector;
</li>
<li>
evictWindow(): it deletes the window by deleting the node in which there was the window and it updates the list.
</li>
