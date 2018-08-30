# 图片上传
## 前台

```
<asp:FileUpload ID="FilePicture" runat="server" Style="width: 99%; height: 20px" onchange="aa()" />
<img id="showImg" src="" alt="" style="width: 100px; height: 80px; margin-top: 5px" /><span>
  ```
  ## 后台上传图片到文件夹中
  ```
        protected void BtnInsert_Click(object sender, EventArgs e)
        {
            MODEL.Materiel MyMateriel = new MODEL.Materiel();
            if (FilePicture.HasFile)
            {
                try
                {
                    string filepath = Server.MapPath("../FileData/");
                    string filename = FilePicture.FileName;
                    string newfile = DateTime.Now.ToFileTime() + filename;

                    if (filename != null && filename != "")
                    {
                        FilePicture.SaveAs(filepath + newfile);
                        string it = Myfunction.Capture(Id, newfile, Keywordlist);
                        System.Web.UI.ScriptManager.RegisterStartupScript(this.FilePicture, this.GetType(), "null", "alert('新增成功');window.location.href='PicSettings.aspx?ID=" + Id + "&Keyword=" + Keywordlist + "'", true);
                        //表示新增成功

                    }
                    else
                    {
                        //表示用户名存在或者新增失败
                        System.Web.UI.ScriptManager.RegisterStartupScript(this.FilePicture, this.GetType(), "null", "alert('新增失败，该物料已存在');", true);
                    }


                }
                catch (Exception ex)
                {

                    System.Web.UI.ScriptManager.RegisterStartupScript(this.FilePicture, this.GetType(), "null", "alert('出现错误,无法上传文件！');", true);

                }

            }
            else
            {

                System.Web.UI.ScriptManager.RegisterStartupScript(this.FilePicture, this.GetType(), "null", "alert('无法上传空的文件！');", true);

            }
        }
        
