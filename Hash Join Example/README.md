# SAS Hash Join

```sas
data new_dataset_name;

    if 0 then set right_dataset; 

    if _n_ = 1 then do;
        declare hash h(hashexp:16, dataset:'right_dataset');
        h.defineKey('key1', 'key2', 'key3', 'key4');
        h.defineData('column_to_join');
        h.defineDone();
    end;

    do until(eof);

        set left_dataset end=eof;

        if h.find() = 0 then output;

        else do;
            call missing(column_to_join);
            output;
        end;

    end;

    stop;

run;
```
