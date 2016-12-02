Originally from http://www.high-flying.co.uk/c-sharp/cache.insert-with-file-dependency-and-callback-on-cache-removal.html

# Cache.Insert with File Dependency and Callback on Cache Removal

Here we look at how to use Cache.Insert to create a cache item and give it a dependency on a file, and then provide a callback method for when the cache is removed.

Cache.Insert

We can use the Cache.Insert() overloaded method to add items to the cache. Cached items mean we can store data (C# objects) in memory on the web server, for instance results from a database query, so that that when we need that data again, we don't need to go back to the database and perform a time consuming operation, we can just get it straight from the server memory in the Cache object. If you want fresh up-to date data, then you'll need to carefully consider using the Cache.

We can set additional parameters such as the AbsoluteExpiration which sets the cache to expire on a particular DateTime value. SlidingExpiration means the time left before removal from the cache is reset every time a user accesses the object unless the specified TimeSpan value has passed.

Here we use Cache.Insert to cache the contents of a text file with no additionl properties set on the cache:


Cache.Insert("MyTextFile",
        File.ReadAllText(Request.PhysicalApplicationPath + "MyTextFile.txt")); 


File Dependency - CacheDependency

So if the data doesn't change and there is a performance hit for retrieving your object of data, using the Cache could be a good option for you. If your data does change, then depending on how frequently, Cache could still be useful. The CacheDependency class allows us to keep the cached item in memory for a time depending on changes to either a file, another cached item, an array of these, or even a SQL database table or results of a query. Should a change occur in the object which the dependency has been set up on, the cached item will be removed.

In the following code, we create a cache of the same text file, except additionally we create a dependency on the text file itself. What that means is that we'll cache the contents of the text file for as long as the server can, or should the text file be changed then we'll delete the cache.


Cache.Insert("MyTextFile",
        File.ReadAllText(Request.PhysicalApplicationPath + "MyTextFile.txt"),
        new System.Web.Caching.CacheDependency(Request.PhysicalApplicationPath + "MyTextFile.txt") ); 


CacheItemRemovedCallback Delegate

The CacheItemRemovedCallback delegate allows to specify a callback method which will be called when our Cached item gets deleted. This is quite handy as it can automate re-populating our Cache object without having to wait for the next call to read the object (which we would have coded such that it had seen the cache is empty and re-populates the cache).

Shown below is the full example, creating a cached object, setting up a dependency on a file, and specifying a callback method to fire when the cached item is deleted (because the file was updated).


using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.IO;
using System.Web.Caching;

namespace Caching
{
    public partial class _Default : System.Web.UI.Page
    {
        // static string available across page requests
        static String message = "";

        public System.Web.Caching.CacheItemRemovedCallback CacheTextFileRemoved = null;

        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                // reset message to blank should it have changed earlier
                message = "";

                CacheTextFileRemoved = new System.Web.Caching.CacheItemRemovedCallback(CacheTextFukeRemovedCallback);

                // create cache entry
                Cache.Insert("MyTextFile",
                    File.ReadAllText(Request.PhysicalApplicationPath + "MyTextFile.txt"),
                    new System.Web.Caching.CacheDependency(Request.PhysicalApplicationPath + "MyTextFile.txt"),
                    System.Web.Caching.Cache.NoAbsoluteExpiration,
                    System.Web.Caching.Cache.NoSlidingExpiration,
                    System.Web.Caching.CacheItemPriority.Default,
                    CacheTextFileRemoved
                );
            }
        }

        protected void Button1_Click(object sender, EventArgs e)
        {
            String textFile = (String)Cache["MyTextFile"] ?? "";

            Literal_TestCache.Text = textFile + message;
        }

        public void CacheTextFukeRemovedCallback(String k, Object v, CacheItemRemovedReason r)
        {
            Literal_AvailableBytes.Text = message;
            message = "<br />Cache removed";
        }
    }
} 
