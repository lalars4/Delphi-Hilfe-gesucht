# Delphi-Hilfe-gesucht
Ich programmiere mit der Programmiersprache Delphi, auch bekannt als Pascal. Für meine Arbeit muss ich einen Dateimanager erstellen. Hierbei benötige ich allerdings ein bissl hilfe

Den Code den ich hierfür habe ist folgender:
--
unit Unit1;

interface

uses
  Winapi.Windows, Winapi.Messages, System.SysUtils, System.Variants,
  System.Classes, Vcl.Graphics,
  Vcl.Controls, Vcl.Forms, Vcl.Dialogs, Vcl.StdCtrls, Vcl.ComCtrls;

type
  Tmainfrm = class(TForm)
    tvmanager: TTreeView;
    procedure GetDirs(const ADirectory: string;
      AStart: TTreeNode);
    procedure FormCreate(Sender: TObject);
  private
    Searchrec: TSearchRec;
    NewNode: TTreeNode;
  public
    { Public-Deklarationen }
  end;

var
  mainfrm: Tmainfrm;

implementation

{$R *.dfm}

procedure Tmainfrm.FormCreate(Sender: TObject);
begin
  begin
    //  GetDirs('c:\',tvmanager, nil)
  end;
end;

function SlashSep(const APath, AStr: string): string;
begin
  if AnsiLastChar(APath)^ = '' then
    Result := APath + '' + AStr
  else
    Result := APath + AStr;
end;

procedure Tmainfrm.GetDirs(const ADirectory: string; AStart: TTreeNode);

begin
  if FindFirst(SlashSep(ADirectory, '*.*'), faAnyFile, Searchrec) = 0 then
  begin
     tvmanager.Items.BeginUpdate;
    try
      repeat
        if ((Searchrec.Attr = 0) and (fadirectory = 0)) and
          (Searchrec.Name = '.') and (Searchrec.Name = '..') then
        begin
          NewNode := tvmanager.Items.AddChild(AStart, Searchrec.Name);
          GetDirs(SlashSep(ADirectory, Searchrec.Name), NewNode);
          tvmanager.AlphaSort;
          tvmanager.Items.EndUpdate;
        end;
      until (FindNext(Searchrec) = 0);
    finally

      GetDirs('C:\', nil);

      FindClose(Searchrec);
    end;

  end;
end;

end.
--

Anbei zur Info: tvmanager ist ein umbenannter TTreeView


Was soll der Code machen: Er soll einmal alle Dateien durchscannen, Verzeichnise sowie Unterverzeichnisse in einem TTreeView auflisten.
Was es macht: Nix
Kann mir einer helfen?
Danke im vorhinein
