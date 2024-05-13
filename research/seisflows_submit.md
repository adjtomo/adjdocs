# SeisFlows Submit

What happens when you run `seisflows submit`?

1. Load `system` module
2. `system.submit()`  
	- `config.import_seisflows`: loads parameters, sets up logger, imports all modules
	- `workflow.check()`: [module.check() for module in modules], checks parameter acceptability, fails if parameters do not pass certain criteria
	- `workflow.setup()`: [module.setup() for module in modules], setup includes mkdir's, loading checkpoints, assigning internal parameters
	- `workflow.run()`: [task() for task in workflow.task_list], runs through all functions defined by the workflow
3. Example Forward workflow
	



