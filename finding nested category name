var products = {
  "categoryList": [
    {
      "_id": "1",
      "name": "electronics",
      "children" : [
        {
          "_id": "2",
          "name": "mobile",
          "parentId": "1",
          "children": [
            {
              "_id": "3",
              "name": "android",
              "parentId": "2",
              "children": []
            },
            {
              "_id": "4",
              "name": "ios",
              "parentId": "2",
              "children": []
            },
          ]
        },
        {
          "_id": "5",
          "name": "television",
          "parentId": "1",
          "children": []
        }
      ],
    },
    {
      "_id": "6",
      "name": "fashion",
      "children" : []
    }
  ]
}

var chindrenFinder = {

  // for keeping track
  currentCategoryObject: {},
  childrenNameArray: [],

  // whether object has children or not 
  hasChildren: function ( object ) {
    return !!object.children;
  },

  // main function to find/search object of specific categoryName
  // this function can be calling outside for finding object
  searchObjectByCategoryName: function(list, categoryName) {
    // reset initial value
    this.currentCategoryObject = {};
    this.findObjectByCategoryName(list, categoryName);
    return this.currentCategoryObject;
  },
  // recursive function for finding object with desired category name
  findObjectByCategoryName: function(list, categoryName) {
    list.forEach(function (eachCategoryObject) {
      if (eachCategoryObject.name == categoryName) {
        this.currentCategoryObject = eachCategoryObject;
        return true;
      } 
      if ( this.hasChildren(eachCategoryObject) ) {
        this.findObjectByCategoryName(eachCategoryObject.children, categoryName);
      }
    }.bind(this));
  },
  // just generating category name from object 
  generateChildrenNameFromObject: function (object, categoryName) {
    this.childrenNameArray.push(object.name);
    if (this.hasChildren(object)) {
      this.generateChildrenName(object.children, categoryName);
    }
  },
  // recursive function for generate categoryName
  generateChildrenName: function (listOrObject, categoryName) {
    if (Array.isArray(listOrObject)) {
      listOrObject.forEach(function(object) {
        this.generateChildrenNameFromObject(object, categoryName);
      }.bind(this))
    }else {
      this.generateChildrenNameFromObject(listOrObject, categoryName);
    }
  },
  // this function can be calling outside for generating categoryName
  getChildrenNameArray: function (list, categoryName) {
    // reset initial value;
    this.childrenNameArray = [];
    var object = this.searchObjectByCategoryName(list, categoryName);
    if (object.name) {
      var cloneObject = Object.assign({}, object);
      this.generateChildrenName(cloneObject);
      return this.childrenNameArray;
    } else {
      return 'category not found';
    }
  }
}

// testing 
console.log( 'test1', chindrenFinder.getChildrenNameArray(products.categoryList, 'electronics') );
console.log( 'test2', chindrenFinder.getChildrenNameArray(products.categoryList, 'mobile') );
console.log( 'test3', chindrenFinder.getChildrenNameArray(products.categoryList, 'television') );
console.log( 'test4', chindrenFinder.getChildrenNameArray(products.categoryList, 'fashion') );
console.log( 'test5', chindrenFinder.getChildrenNameArray(products.categoryList, 'not') );
