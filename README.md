# JsonPeek.MsBuild

Forked from [https://bitbucket.org/Manishkp/jsonpeek.msbuild]() which appears to be abandoned.

JsonPoke and JsonPeek build tasks:
# Usage

JSON Poke:

     // Write to file from explicit value
     <JsonPoke JsonInputPath="$(MSBuildProjectDirectory)\Project.json" JValue="Empty-FromTest1" JPath="Project.Name"></JsonPoke>
     
     // Write to file from MSBuild array
     <JsonPoke JsonInputPath="$(MSBuildProjectDirectory)\Project.json" JArray="@(TestArray1)" JPath="Project.TestArray" Metadata="MyProp;Identity"></JsonPoke>
     
     // Write to file using explicit array
     <JsonPoke JsonInputPath="$(MSBuildProjectDirectory)\Project.json" JArray="t11.txt;t22.txt" JPath="Project.TestArray1"></JsonPoke>
     
     // Write to file using a complex object
     <JsonPoke JsonInputPath="$(MSBuildProjectDirectory)\Project.json" JObject="@(BuildNumber)" JPath="Project.TestObject" Metadata="Major;Minor;Build">
     
JsonPeek:

     <PropertyGroup>
       <JsonContent>
         <![CDATA[{
         "Projects":[
           { "Name": "P1",  "OutputFile": "P1.json", "Variables": [ "Var1", "Var2" ] },
           { "Name": "P2", "OutputFile": "P2.json", "Variables": [ "Var1", "Var2" ] }
          ]
         ]]>
       </JsonContent>
     </PropertyGroup>
     
     <JsonPeek JPath="$.Projects" JsonContent="$(JsonContent)">
      <Output TaskParameter="Result" ItemName="TestProjects" />
     </JsonPeek>
     
     <Message Text="Project.IncludedLibraryVariableSetIds[?(@.Name == 'Lib-69')].Value : @(Lib69Value)" />
     <Message Text="Project values: %(TestProjects.Name)" />
