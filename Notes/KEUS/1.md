class GlobalContextManager {
	globalContext
	siteId
	nodeId
	environment
	...

	public static refresh(){
		// logic to update global context
	} 

	public static getContext(){
		return this.globalContext
	}
}

GlobalContextManager is optional dependency for logger:
class _Logger {
	
	private enrichLog(args: LogInput) {

        args = typeof args === "string" ? { msg: args } : args

        if (process.env.SKIP_LOG_CONTEXT == "true") {
            return args;
        }

        return { ...args, ...GlobalContextManager.getContext(), ...contextStore.getStore(), ...this.settings.context }
    }
	
}