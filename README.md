# envfile

POSIX-compatible script – like `env` – to run a program in an environment modified by values set in a *file* at the specified path.

This achieves the same as:

    env NAME1=VALUE1 NAME2=VALUE2 make -d info

or, in shells which support it, omitting `env`:

    NAME1=VALUE1 NAME2=VALUE2 make -d info

with the distinction that these values may be persisted to a file:

    # dev.env

    # The first setting
    NAME1=VALUE1

    # Oh and this is the second one
    NAME2=VALUE2

and loaded into the execution environment:

    envfile dev.env make -d info

like in the previous, on-the-fly examples, without polluting the user's shell environment.

## Alternatives

It should be noted that something similar may be achieved with subshells:

    (. dev.env && echo $NAME1)

which does not pollute the invoking environment.

However, the above only works for inline variable references, such as `echo $NAME1`. Any subprocess, such as `make -d info`, will not have access to the environment values declared by the environment file, **unless** this file uses `export`:

    # dev.env

    # The first setting
    export NAME1=VALUE1

    # Oh and this is the second one
    export NAME2=VALUE2
