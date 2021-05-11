This repo reproduces issue with docker-compose on Apple silicon.

### Steps to reproduce

1. Run `yarn start`. The output should be like:
```
yarn run v1.22.10
$ node index.js
{
  argv: [
    '/opt/homebrew/Cellar/node/16.1.0/bin/node',
    '/Users/myuser/docker-m1-node-argv/index.js'
  ]
}
✨  Done in 0.31s.
```
This is the expected output from the `index.js` script. `argv` array contains only two arguments.

2. Run `docker compose up`. The output is:
```
[+] Running 1/0
 ⠿ Container docker-m1-node-argv_test_1  Created                                   0.0s
Attaching to test_1
test_1  | yarn run v1.22.5
test_1  | $ node index.js yarn start
test_1  | { argv: [ '/usr/local/bin/node', '/index.js', 'yarn', 'start' ] }
test_1  | Done in 0.05s.
test_1 exited with code 0
```

As we con see `argv` array contain two extra elements: `yarn`, `start`.
This is reproducible only when `docker-compose.override.yaml` is present.