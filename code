function checkCashRegister(price, cash, cid) {
  let result = {
    status: 'OPEN',
    change: []  
  };
  //everyting 100x to avoid decimal rounding problems
  let unitValue = {
    "PENNY": 1,
    "NICKEL": 5,
    "DIME": 10,
    "QUARTER": 25,
    "ONE": 100,
    "FIVE": 500,
    "TEN" : 1000,
    "TWENTY": 2000,
    "ONE HUNDRED": 10000
  };

  //creating objects from cid array
  let units = {}
  cid.forEach((i) => {units[i[0]] = {amount: i[1] * 100, value: unitValue[i[0]]}});

  let money = 0;
  let change = (cash - price) * 100
  for (let i = 0; i < cid.length; i++) {
    money += (cid[i][1] * 100)
  }
  
  if (money == change) {
    result['status'] = "CLOSED";
    result['change'] = cid;
    return result;
  }
  
  if (money < change) {
    result['status'] = "INSUFFICIENT_FUNDS";
    result['change'] = [];
    return result;
  }
  
  // removing units that are to big
  for (let unit in units) {
    if (units[unit]['value'] > change) {
      money -= units[unit]['amount'];
    }
  }
  
  if (money < change) {
    result['status'] = "INSUFFICIENT_FUNDS";
    result['change'] = [];
    return result;
  };

  //filling up result['change'] array
  for (let i = cid.length - 1; i >= 0; i--) {
    let counter = 0;
    while (change >= units[cid[i][0]]['value'] && units[cid[i][0]]['amount'] > 0) {
      change -= units[cid[i][0]]['value'];
      money -= units[cid[i][0]]['value'];
      units[cid[i][0]]['amount'] -= units[cid[i][0]]['value'];
      counter++
    }
    if (counter > 0) result['change'].push([cid[i][0], units[cid[i][0]]['value'] * counter / 100]);    
  };

  if (change > 1) {
    result['status'] = "INSUFFICIENT_FUNDS";
    result['change'] = [];
    return result;
  };
  return result
}

console.log(checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]));
