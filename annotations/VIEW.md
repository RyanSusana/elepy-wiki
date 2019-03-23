# @View
The view annotation points to the class that handles how RestModels are viewed, and controlled in the CMS. It points to a class that implements the RestModelView interface. This Interface has one abstract method `#renderView(ModelDescription)`, it returns String. The String it returns is essentially the HTML content in the CMS for a specific RestModel.

Example usage:
https://elepy.com/docs/custom-views