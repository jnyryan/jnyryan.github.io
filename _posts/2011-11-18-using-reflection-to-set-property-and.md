---
title: "Using Reflection to set Property and Field values"
layout: "post"
permalink: "/2011/11/using-reflection-to-set-property-and.html"
uuid: "1292172880875155966"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-1292172880875155966"
date: "2011-11-18 14:23:00"
updated: "2011-12-01 15:23:42"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "1292172880875155966"
    comments: "0"
categories: playing-with-technology
tags: [C#]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

When dealing with legacy code I find it invaluable to have a way of accessing private internal members to write. Here's some very handy code that will do just that. And for goo measure, i've included some unit tests.

``` c
///////////////////////////////////////////////////////////////////////////////////////////////////
// Subtext WebLog
// 
// Subtext is an open source weblog system that is a fork of the .TEXT
// weblog system.
//
// For updated news and information please visit http://subtextproject.com/
// Subtext is hosted at SourceForge at http://sourceforge.net/projects/subtext
// The development mailing list is at subtext-devs@lists.sourceforge.net 
//
// This project is licensed under the BSD license.  See the License.txt file for more information.
///////////////////////////////////////////////////////////////////////////////////////////////////


using System;
using System.Reflection;
using Components.Infrastructure.Common;


namespace Common.ReflectionHelper
{
 ///
 /// Helper class to simplify common reflection tasks.
 ///
 public static class ReflectionHelper
 {
  ///
  /// Sets the value of the private static member.
  ///
  public static void SetStaticFieldValue(string fieldName, Type type, T value)
  {
   FieldInfo field = type.GetField(fieldName, BindingFlags.NonPublic | BindingFlags.Static);
   if (field == null)
    throw new ArgumentException(string.Format("Could not find the private instance field '{0}'", fieldName));


   field.SetValue(null, value);
  }


  ///
  /// Sets the value of the private static member.
  ///
  public static void SetStaticFieldValue(string fieldName, string typeName, T value)
  {
   Type type = Type.GetType(typeName, true);
   FieldInfo field = type.GetField(fieldName, BindingFlags.NonPublic | BindingFlags.Static);
   if (field == null)
    throw new ArgumentException(string.Format("Could not find the private instance field '{0}'", fieldName));


   field.SetValue(null, value);
  }


///
/// Returns the value of the private member specified.
///
/// Name of the member.
/// Type of the member.
public static T GetStaticFieldValue(string fieldName, Type type)
{
    FieldInfo field = type.GetField(fieldName, BindingFlags.NonPublic | BindingFlags.Static);
    if (field != null)
    {
        return (T)field.GetValue(type);
    }
    return default(T);
}


///
/// Returns the value of the private member specified.
///
/// Name of the member.
///
public static T GetStaticFieldValue(string fieldName, string typeName)
{
    Type type = Type.GetType(typeName, true);
    FieldInfo field = type.GetField(fieldName, BindingFlags.NonPublic | BindingFlags.Static);
    if (field != null)
    {
        return (T)field.GetValue(type);
    }
    return default(T);
}


///
/// Sets the value of the private member specified.
///
/// Name of the member.
/// The object that contains the member.
/// The value to set the member to.
public static void SetPrivateInstanceFieldValue(string memberName, object source, object value)
{
    FieldInfo field = source.GetType().GetField(memberName, BindingFlags.GetField | BindingFlags.NonPublic | BindingFlags.Instance);
    if (field == null)
    throw new ArgumentException(string.Format("Could not find the private instance field '{0}'", memberName));


    field.SetValue(source, value);
}


///
/// Sets the value of the private member specified.
///
/// Name of the property.
/// The object that contains the property.
/// The value to set the property to.
public static void SetPrivateInstancePropertyValue(string propName, object source, object value)
{
    PropertyInfo property = source.GetType().GetProperty(propName, BindingFlags.GetField | BindingFlags.NonPublic | BindingFlags.Instance);
    if (property == null)
        throw new ArgumentException(string.Format("Could not find the private instance property '{0}'", propName));


    property.SetValue(source, value, BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.SetProperty | BindingFlags.Instance, null, null, null);
}


///
/// Returns the value of the private member specified.
///
/// Name of the member.
/// The object that contains the member.
public static object GetStaticField(string fieldName, object source)
{
    return GetStaticField(fieldName, source, source.GetType());
}


///
/// Returns the value of the private member specified.
///
/// Name of the member.
/// The object that contains the member.
///
public static object GetStaticField(string fieldName, object source, Type type)
{
    FieldInfo field = type.GetField(fieldName, BindingFlags.NonPublic | BindingFlags.Static);
    if(field != null)
    {
        return field.GetValue(type);
    }
    return null;
}


///
/// Returns the value of the private member specified.
///
/// Name of the member.
/// The object that contains the member.
public static object GetPrivateInstanceField(string memberName, object source)
{
FieldInfo field = source.GetType().GetField(memberName, BindingFlags.GetField | BindingFlags.NonPublic | BindingFlags.Instance);
if(field != null)
{
return field.GetValue(source);
}
return null;
}


    ///
    /// Returns the value of the private member specified.
    ///
    /// Name of the member.
    /// The object that contains the member.
    public static object GetPrivateInstanceProperty(string propName, object source)
    {
        PropertyInfo prop = source.GetType().GetProperty(propName, BindingFlags.GetProperty | BindingFlags.NonPublic | BindingFlags.Instance);
        if (prop != null)
        {
            return prop.GetValue(source, BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.SetProperty | BindingFlags.Instance, null, null, null);
        }
        return null;
    }


    public static object RunStaticMethod(Type t, string strMethod, object[] objParams)
    {
        BindingFlags eFlags = BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic;
        return RunMethod(t, strMethod, null, objParams, eFlags);
    }


    public static object RunInstanceMethod(Type t, string strMethod, object objInstance, object[] aobjParams)
    {
        BindingFlags eFlags = BindingFlags.Instance | BindingFlags.Public |
                              BindingFlags.NonPublic;
        return RunMethod(t, strMethod, objInstance, aobjParams, eFlags);
    }


    private static object RunMethod(Type t, string strMethod, object objInstance, object[] objParams,
                                    BindingFlags eFlags)
    {
        MethodInfo m = t.GetMethod(strMethod, eFlags);
        if (m == null)
        {
            throw new ArgumentException("There is no method '" + strMethod + "' for type '" + t + "'.");
        }


        object objRet = m.Invoke(objInstance, objParams);
        return objRet;
    }
 }
}




///////////////////////////////////////////////////////////////////////////////////////////////////
// Unit Test 

///////////////////////////////////////////////////////////////////////////////////////////////////



namespace  Common.UnitTests.ReflectionHelper {
    internal class TestClass
    {
        private string myField = "This is my initial value";         private String MyProperty
        {
            get { return myField; }
            set { myField = value; }
        }
    }
    [TestFixture]
    public class ReflectionHelperTests
    {
        [Test]
        public void PrivateInstanceFieldsTest()
        {
            var testValue = "This is my new Value";
            var myTestClass = new TestClass();
            var result = ReflectionHelper.GetPrivateInstanceField("myField", myTestClass);
            ReflectionHelper.SetPrivateInstanceFieldValue("myField", myTestClass, testValue);
            result = ReflectionHelper.GetPrivateInstanceField("myField", myTestClass);
            Assert.AreEqual(testValue, result);
        }


        [Test]
        public void PrivateInstancePropertyTest()
        {
            var testValue = "This is my new Value";
            var myTestClass = new TestClass();
            ReflectionHelper.SetPrivateInstancePropertyValue("MyProperty", myTestClass, testValue);
            var result = ReflectionHelper.GetPrivateInstanceProperty("MyProperty", myTestClass);
            Assert.AreEqual(testValue, result);
        }
    }
}

```