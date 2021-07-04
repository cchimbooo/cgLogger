cgLogger is a package that helps the customization of the default gorm (v2) logger.

This allows the user to implement a function to be executed given a condition.

The main recommendation is to use this functions to log the data differently.

Ex: sentry / file

The conditions are: 

    Error: ErrorTrigger(func)
    
    Sql Take more than x Seconds:  SlowTrigger(func, x)
    
    Always: AlwaysTrigger(func)


The function that those methods receive have the following signature:

    func(g GormInfos)
    
    // GormInfos are the data passed to the custom functions
    type GormInfos struct {
        Location      string
        AffectedRows  int64
        QueryDuration float64
        Sql           string
        Err           error
    }   



Is not recommended changing this functions during the execution of a program.
That said if you need to change it you should change the logger itself.

To implement that the functions LogMode() and FixTriggers() will return a gorm logger interface.
That said the methods xTrigger() won't be available.

(OBS: I decided to keep this in that way so by "default" the user will lock the use of the triggers functions,
and if he is aware of the risk he can keep those)