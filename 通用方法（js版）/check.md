```javascript
'use strict';

const checkPhone = (data) => {
	const reg = /^1[3-9][0-9]{9}$/;
	if(!reg.test(data)) {
		return false;
	}
	return true;
};

const checkEmail = (data) => {
	const reg = /^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
	if(!reg.test(data)) {
		return false;
	}
	return true;
};

export default {
	checkPhone,
	checkEmail
}
```

