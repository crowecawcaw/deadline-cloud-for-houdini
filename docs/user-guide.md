# User guide

## Parallel vs. Sequential Rendering

For many types of nodes, frames can be rendered independently and in any order. For others like simulations, each frame depends on the result of the previous frame and must be rendered sequentially. The submitter chooses a rendering strategy for each node based on its type, but also allows you to override the default.

For parallel rendering, each frame has its own task, and the tasks will be distributed across available workers. For sequential rendering, all frames for a node are rendered in a single task running on a single worker.

By default, if a node is a geometry node with the "Initialize Simulation OPs" option enabled, it will render sequentially. Otherwise the node will render in parallel.

### Overriding the render strategy

You can override the render strategy be creating a `deadline_cloud_render_strategy` parameter with a value of either `SEQUENTIAL` or `PARALLEL`.

To add a parameter to a node:
1. Right click a node in the `out` context, select "Parameters and Channels" then click "Edit Parameter Interface".
2. Under "Create Parameters", select "Ordered Menu" and click the right arrow to add it to the "Existing Parameters" list.
3. Select the new parameter under "Existing Parameters", then edit its configuration under "Parameter Description":
    
    a. Under the "Parameter" tab, set "Name" to `deadline_cloud_render_strategy` and "Label" to "Deadline Cloud Render Strategy"
    
    b. Under the Menu tab, add menu items for:

    | Token      | Label      |
    | ---------- | ---------- |
    | SEQUENTIAL | Sequential |
    | PARALLEL   | Parallel   |
4. Click Accept.
5. Now in the parameter editor for your node, you'll find the new "Deadline Cloud Render Strategy" menu which specifies the submitter behavior.