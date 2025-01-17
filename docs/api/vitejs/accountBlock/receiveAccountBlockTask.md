
# Auto-Receive AccountBlock

Enable auto-receive on the account for incoming transactions

## Constructor

- **Constructor Parameters**
    * `__namedParameters: object`        
        - `address: Address` Address of account, mandatory
        - `provider: ViteAPI` `ViteAPI` instance
        - `privateKey: Hex` privateKey

- **Example**
```javascript
import { accountBlock } from '@vite/vitejs';

const { ReceiveAccountBlockTask } = accountBlock;

const ReceiveTask = new ReceiveAccountBlockTask({
    address: 'your address',
    privateKey: 'your privateKey',
    provider: viteProvider,
});

ReceiveTask.onSuccess((result) => {
    console.log('success', result);
    // No unreceived accountBlocks, stop receiving-task
    if (!result.accountBlockList) {
        ReceiveTask.stop();
    }
});
ReceiveTask.onError((error) => {
    console.log('error', error);
});
ReceiveTask.start({
    checkTime: 3000,
    transctionNumber: 10
});
```

## Methods

### start
Start auto-receive account blocks

- **Parameters** 
    * `__namedParameters: object`
        - `checkTime?: number` Polling interval of unreceived transactions. Default is 3000(ms)
        - `transctionNumber?: number` Transactions handled in each poll. Default is 5

- **Example**
```javascript
import { accountBlock } from '@vite/vitejs';

const { ReceiveAccountBlockTask } = accountBlock;

const ReceiveTask = new ReceiveAccountBlockTask({
    address: 'your address',
    privateKey: 'your privateKey',
    provider: viteProvider,
});

ReceiveTask.start({
    checkTime: 3000,
    transctionNumber: 10
});
```

### stop
Stop auto-receive account blocks

- **Example**
```javascript
import { accountBlock } from '@vite/vitejs';

const { ReceiveAccountBlockTask } = accountBlock;

const ReceiveTask = new ReceiveAccountBlockTask({
    address: 'your address',
    privateKey: 'your privateKey',
    provider: viteProvider,
});

ReceiveTask.start({
    checkTime: 3000,
    transctionNumber: 10
});
ReceiveTask.stop();
```

### onError
Receive failed handler

- **Parameters** 
    * `errorCB: Function` Event handler on receive failure

- **error** Error message
    - `status: 'error'`
    - `message: string` Error message
    - `timestamp: number` Timestamp
    - `unreceivedHash?: Hex` Hash of AccountBlock that was received unsuccessfully
    - `error: any` RPC error message

- **Example**
```javascript
import { accountBlock } from '@vite/vitejs';

const { ReceiveAccountBlockTask } = accountBlock;

const ReceiveTask = new ReceiveAccountBlockTask({
    address: 'your address',
    privateKey: 'your privateKey',
    provider: viteProvider,
});

ReceiveTask.onError((error) => {
    console.log('error', error);
});
ReceiveTask.start({
    checkTime: 3000,
    transactionNumber: 10
});
```

### onSuccess
Receive succeeded handler

- **Parameters** 
    * `successCB: Function` Event handler on receive success

- **success** Success message
    - `status: 'ok'`
    - `message: string` Success message
    - `timestamp: number` Timestamp
    - `accountBlockList?: AccountBlock[]` AccountBlockList that has been received

- **Example**
```javascript
import { accountBlock } from '@vite/vitejs';

const { ReceiveAccountBlockTask } = accountBlock;

const ReceiveTask = new ReceiveAccountBlockTask({
    address: 'your address',
    privateKey: 'your privateKey',
    provider: viteProvider,
});

ReceiveTask.onSuccess((result) => {
    console.log('success', result);
});
ReceiveTask.start({
    checkTime: 3000,
    transactionNumber: 10
});
```
